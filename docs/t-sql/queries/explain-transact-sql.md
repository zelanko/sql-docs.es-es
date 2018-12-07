---
title: EXPLAIN (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: conceptual
ms.assetid: 4846a576-57ea-4068-959c-81e69e39ddc1
author: shkale-msft
ms.author: shkale
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 486d03addff39a0377298dcd1ddfb768046f2aa1
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/27/2018
ms.locfileid: "52417806"
---
# <a name="explain-transact-sql"></a>EXPLAIN (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Devuelve el plan de consulta para una instrucción [!INCLUDE[ssDW](../../includes/ssdw-md.md)] [!INCLUDE[DWsql](../../includes/dwsql-md.md)] sin ejecutarla. Use **EXPLAIN** para obtener una vista previa de las operaciones que requerirán movimiento de datos y ver los costos estimados de las operaciones de consulta.  
  
 Para obtener más información sobre los planes de consulta, vea "Descripción de los planes de consulta" en la [!INCLUDE[pdw-product-documentation_md](../../includes/pdw-product-documentation-md.md)].  
  
## <a name="syntax"></a>Sintaxis  
  

```  
EXPLAIN SQL_statement  
[;]  
```  
  
## <a name="arguments"></a>Argumentos  
 *SQL_statement*  
 La instrucción [!INCLUDE[DWsql](../../includes/dwsql-md.md)] en la que se ejecutará **EXPLAIN**. *SQL_statement* puede ser cualquiera de estos comandos: **SELECT**, **INSERT**, **UPDATE**, **DELETE**, **CREATE TABLE AS SELECT**, **CREATE REMOTE TABLE**.  
  
## <a name="permissions"></a>Permisos  
 Requiere el permiso **SHOWPLAN** y el permiso para ejecutar *SQL_statement*. Vea [Permisos: GRANT, DENY, REVOKE &#40;Azure SQL Data Warehouse, Almacenamiento de datos paralelos&#41;](../../t-sql/statements/permissions-grant-deny-revoke-azure-sql-data-warehouse-parallel-data-warehouse.md).  
  
## <a name="return-value"></a>Valor devuelto  
 El valor devuelto del comando **EXPLAIN** es un documento XML con la estructura que se muestra a continuación. En este documento XML se enumeran todas las operaciones en el plan de consulta para la consulta especificada, delimitadas por la etiqueta `<dsql_operation>`. El valor devuelto es de tipo **nvarchar(max)**.  
  
 En el plan de consulta devuelto se representan instrucciones SQL secuenciales; cuando la consulta lo ejecuta puede implicar operaciones en paralelo, por lo que es posible que algunas de las instrucciones secuenciales que se muestran se ejecuten al mismo tiempo.  
  
```  
\<?xml version="1.0" encoding="utf-8"?>  
<dsql_query>  
  <sql>. . .</sql>  
  <params />  
  <dsql_operations>  
    <dsql_operation>  
     . . .      
    </dsql_operation>  
    [ . . . n ]  
  <dsql_operations>  
</dsql_query>  
```  
  
 Las etiquetas XML contienen esta información:  
  
|Etiqueta XML|Resumen, atributos y contenido|  
|-------------|--------------------------------------|  
|\<dsql_query>|Elemento de documento o nivel superior.|
|\<sql>|Muestra *SQL_statement*.|  
|\<params>|Esta etiqueta no se usa actualmente.|  
|\<dsql_operations>|Resume y contiene los pasos de consulta, e incluye información del costo de la consulta. También contiene todos los bloques `<dsql_operation>`. Esta etiqueta contiene información de recuento para toda la consulta:<br /><br /> `<dsql_operations total_cost=total_cost total_number_operations=total_number_operations>`<br /><br /> *costo_total* es el tiempo total estimado para que se ejecute la consulta, en milisegundos.<br /><br /> *número_total_de_operaciones* es el número total de operaciones para la consulta. Una operación que se va a ejecutar en paralelo y en varios nodos se cuenta como una única operación.|  
|\<dsql_operation>|Describe una única operación dentro del plan de consulta. La etiqueta \<dsql_operation> contiene el tipo de operación como un atributo:<br /><br /> `<dsql_operation operation_type=operation_type>`<br /><br /> *tipo_de_operación* es uno de los valores encontrados en [Consulta de datos (PDW de SQL Server)](https://msdn.microsoft.com/3f4f5643-012a-4c36-b5ec-691c4bbe668c).<br /><br /> El contenido del bloque `\<dsql_operation>` depende del tipo de operación.<br /><br /> Vea la tabla siguiente.|  
  
|Tipo de operación|Contenido|Ejemplo|  
|--------------------|-------------|-------------|  
|BROADCAST_MOVE, DISTRIBUTE_REPLICATED_TABLE_MOVE, MASTER_TABLE_MOVE, PARTITION_MOVE, SHUFFLE_MOVE y TRIM_MOVE|Elemento `<operation_cost>`, con estos atributos. Los valores solo reflejan la operación local:<br /><br /> -   *costo* es el costo del operador local y muestra el tiempo estimado para que se ejecute la operación, en milisegundos.<br />-   *costo_acumulativo* es la suma de todas las operaciones encontradas en el plan incluidos los valores sumados de las operaciones en paralelo, en milisegundos.<br />-   *promedio_de_tamaño_de_fila* es el tamaño de fila medio estimado (en bytes) de las filas que se recuperan y pasan durante la operación.<br />-   *filas_de_salida* es la cardinalidad de salida (nodo) y muestra el número de filas de salida.<br /><br /> `<location>`: los nodos o las distribuciones en los que se realizará la operación. Las opciones son: “Control”, “ComputeNode”, “AllComputeNodes”, “AllDistributions”, “SubsetDistributions”, “Distribution” y “SubsetNodes”.<br /><br /> `<source_statement>`: los datos de origen para el movimiento aleatorio.<br /><br /> `<destination_table>`: la tabla temporal interna a la que se moverán los datos.<br /><br /> `<shuffle_columns>`: (solo aplicable a las operaciones de SHUFFLE_MOVE). Una o varias columnas que se usarán como las columnas de distribución para la tabla temporal.|`<operation_cost cost="40" accumulative_cost="40" average_rowsize = "50" output_rows="100"/>`<br /><br /> `<location distribution="AllDistributions" />`<br /><br /> `<source_statement type="statement">SELECT [TableAlias_3b77ee1d8ccf4a94ba644118b355db9d].[dist_date] FROM [qatest].[dbo].[flyers] [TableAlias_3b77ee1d8ccf4a94ba644118b355db9d]       </source_statement>`<br /><br /> `<destination_table>Q_[TEMP_ID_259]_[PARTITION_ID]</destination_table>`<br /><br /> `<shuffle_columns>dist_date;</shuffle_columns>`|  
|CopyOperation|`<operation_cost>`: vea `<operation_cost>` más arriba.<br /><br /> `<DestinationCatalog>`: el nodo o nodos de destino.<br /><br /> `<DestinationSchema>`: el esquema de destino en DestinationCatalog.<br /><br /> `<DestinationTableName>`: nombre de la tabla de destino o “TableName”.<br /><br /> `<DestinationDatasource>`: el nombre o la información de conexión del origen de datos de destino.<br /><br /> `<Username>` y `<Password>`: estos campos indican que pueden ser necesarios un nombre de usuario y una contraseña para el destino.<br /><br /> `<BatchSize>`: el tamaño del lote para la operación de copia.<br /><br /> `<SelectStatement>`: la instrucción SELECT que usa para realizar la copia.<br /><br /> `<distribution>`: la distribución donde se realiza la copia.|`<operation_cost cost="0" accumulative_cost="0" average_rowsize="4" output_rows="1" />`<br /><br /> `<DestinationCatalog>master</DestinationCatalog>`<br /><br /> `<DestinationSchema>dbo</DestinationSchema>`<br /><br /> `<DestinationTableName>[TableName]</DestinationTableName>`<br /><br /> `<DestinationDatasource>localhost, 8080</DestinationDatasource>`<br /><br /> `<Username>...</Username>`<br /><br /> `<Password>...</Password>`<br /><br /> `<BatchSize>6000</BatchSize>`<br /><br /> `<SelectStatement>SELECT T1_1.c1 AS c1 FROM [qatest].[dbo].[gigs] AS T1_1</SelectStatement>`<br /><br /> `<distribution>ControlNode</distribution>`|  
|MetaDataCreate_Operation|`<source_table>`: la tabla de origen para la operación.<br /><br /> `<destionation_table>`: la tabla de destino para la operación.|`<source_table>databases</source_table>`<br /><br /> `<destination_table>MetaDataCreateLandingTempTable</destination_table>`|  
|ON|`<location>`: vea `<location>` más arriba.<br /><br /> `<sql_operation>`: identifica el comando SQL que se va a ejecutar en un nodo.|`<location permanent="false" distribution="AllDistributions">Compute</location>`<br /><br /> `<sql_operation type="statement">CREATE TABLE [tempdb].[dbo]. [Q_[TEMP_ID_259]]_ [PARTITION_ID]]]([dist_date] DATE) WITH (DISTRIBUTION = HASH([dist_date]),) </sql_operation>`|  
|RemoteOnOperation|`<DestinationCatalog>`: el catálogo de destino.<br /><br /> `<DestinationSchema>`: el esquema de destino en DestinationCatalog.<br /><br /> `<DestinationTableName>`: nombre de la tabla de destino o “TableName”.<br /><br /> `<DestinationDatasource>`: el nombre del origen de datos de destino.<br /><br /> `<Username>` y `<Password>`: estos campos indican que pueden ser necesarios un nombre de usuario y una contraseña para el destino.<br /><br /> `<CreateStatement>`: la instrucción de creación de tabla para la base de datos de destino.|`<DestinationCatalog>master</DestinationCatalog>`<br /><br /> `<DestinationSchema>dbo</DestinationSchema>`<br /><br /> `<DestinationTableName>TableName</DestinationTableName>`<br /><br /> `<DestinationDatasource>DestDataSource</DestinationDatasource>`<br /><br /> `<Username>...</Username>`<br /><br /> `<Password>...</Password>`<br /><br /> `<CreateStatement>CREATE TABLE [master].[dbo].[TableName] ([col1] BIGINT) ON [PRIMARY] WITH(DATA_COMPRESSION=PAGE);</CreateStatement>`|  
|RETURN|`<resultset>`: el identificador del conjunto de resultados.|`<resultset>RS_19</resultset>`|  
|RND_ID|`<identifier>`: el identificador del objeto que se ha creado.|`<identifier>TEMP_ID_260</identifier>`|  
  
## <a name="limitations-and-restrictions"></a>Limitaciones y restricciones  
 **EXPLAIN** solo se puede aplicar a consultas *optimizables*, que son las que se pueden mejorar o modificar en función de los resultados de un comando **EXPLAIN**. Los comandos **EXPLAIN** admitidos se enumeran anteriormente. Cualquier intento de usar **EXPLAIN** con un tipo de consulta no admitido devolverá un error o mostrará la consulta.  
  
 **EXPLAIN** no se admite en una transacción de usuario.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se muestra un comando **EXPLAIN** ejecutado en una instrucción **SELECT** y el resultado XML.  
  
 **Envío de una instrucción EXPLAIN**  
  
 El comando enviado para este ejemplo es el siguiente:  
  
```  
-- Uses AdventureWorks  
  
EXPLAIN   
    SELECT CAST (AVG(YearlyIncome) AS int) AS AverageIncome,   
        CAST(AVG(FIS.SalesAmount) AS int) AS AverageSales,   
        G.StateProvinceName, T.SalesTerritoryGroup  
    FROM dbo.DimGeography AS G  
    JOIN dbo.DimSalesTerritory AS T  
        ON G.SalesTerritoryKey = T.SalesTerritoryKey  
    JOIN dbo.DimCustomer AS C  
        ON G.GeographyKey = C.GeographyKey  
    JOIN dbo.FactInternetSales AS FIS  
        ON C.CustomerKey = FIS.CustomerKey  
    WHERE T.SalesTerritoryGroup IN ('North America', 'Pacific')  
        AND Gender = 'F'  
    GROUP BY G.StateProvinceName, T.SalesTerritoryGroup  
    ORDER BY AVG(YearlyIncome) DESC;  
GO  
```  
  
 Después de ejecutar la instrucción mediante la opción **EXPLAIN**, en la pestaña de mensaje se presenta una sola línea titulada **explain** y que empieza con el texto XML `\<?xml version="1.0" encoding="utf-8"?>`. Haga clic en el código XML para abrir todo el texto en una ventana XML. Para entender mejor los comentarios siguientes, debe activar la presentación de los números de línea en SSDT.  
  
#### <a name="to-turn-on-line-numbers"></a>Para activar los números de línea  
  
1.  Con el resultado que aparece en la pestaña **explain** de SSDT, en el menú **Herramientas**, seleccione **Opciones**.  
  
2.  Expanda la sección **Editor de texto**, expanda **XML** y, después, haga clic en **General**.  
  
3.  En el área **Presentación**, active **Números de línea**.  
  
4.  Haga clic en **Aceptar**.  
  
 **Resultado del ejemplo de EXPLAIN**  
  
 El resultado XML del comando **EXPLAIN** con los números de fila activados es el siguiente:  
  
```  
1  \<?xml version="1.0" encoding="utf-8"?>  
2  <dsql_query>  
3    <sql>SELECT CAST (AVG(YearlyIncome) AS int) AS AverageIncome,   
4          CAST(AVG(FIS.SalesAmount) AS int) AS AverageSales,   
5          G.StateProvinceName, T.SalesTerritoryGroup  
6      FROM dbo.DimGeography AS G  
7      JOIN dbo.DimSalesTerritory AS T  
8          ON G.SalesTerritoryKey = T.SalesTerritoryKey  
9      JOIN dbo.DimCustomer AS C  
10          ON G.GeographyKey = C.GeographyKey  
11      JOIN dbo.FactInternetSales AS FIS  
12          ON C.CustomerKey = FIS.CustomerKey  
13      WHERE T.SalesTerritoryGroup IN ('North America', 'Pacific')  
14          AND Gender = 'F'  
15      GROUP BY G.StateProvinceName, T.SalesTerritoryGroup  
16      ORDER BY AVG(YearlyIncome) DESC</sql>  
17    <dsql_operations total_cost="0.926237696" total_number_operations="9">  
18      <dsql_operation operation_type="RND_ID">  
19        <identifier>TEMP_ID_16893</identifier>  
20      </dsql_operation>  
21      <dsql_operation operation_type="ON">  
22        <location permanent="false" distribution="AllComputeNodes" />  
23        <sql_operations>  
24          <sql_operation type="statement">CREATE TABLE [tempdb].[dbo].[TEMP_ID_16893] ([CustomerKey] INT NOT NULL, [GeographyKey] INT, [YearlyIncome] MONEY ) WITH(DATA_COMPRESSION=PAGE);</sql_operation>  
25        </sql_operations>  
26      </dsql_operation>  
27      <dsql_operation operation_type="BROADCAST_MOVE">  
28        <operation_cost cost="0.121431552" accumulative_cost="0.121431552" average_rowsize="16" output_rows="31.6228" />  
29        <source_statement>SELECT [T1_1].[CustomerKey] AS [CustomerKey],  
30         [T1_1].[GeographyKey] AS [GeographyKey],  
31         [T1_1].[YearlyIncome] AS [YearlyIncome]  
32  FROM   (SELECT [T2_1].[CustomerKey] AS [CustomerKey],  
33                 [T2_1].[GeographyKey] AS [GeographyKey],  
34                 [T2_1].[YearlyIncome] AS [YearlyIncome]  
35          FROM   [AdventureWorksPDW2012].[dbo].[DimCustomer] AS T2_1  
36          WHERE  ([T2_1].[Gender] = CAST (N'F' COLLATE Latin1_General_100_CI_AS_KS_WS AS NVARCHAR (1)) COLLATE Latin1_General_100_CI_AS_KS_WS)) AS T1_1</source_statement>  
37        <destination_table>[TEMP_ID_16893]</destination_table>  
38      </dsql_operation>  
39      <dsql_operation operation_type="RND_ID">  
40        <identifier>TEMP_ID_16894</identifier>  
41      </dsql_operation>  
42      <dsql_operation operation_type="ON">  
43        <location permanent="false" distribution="AllDistributions" />  
44        <sql_operations>  
45          <sql_operation type="statement">CREATE TABLE [tempdb].[dbo].[TEMP_ID_16894] ([StateProvinceName] NVARCHAR(50) COLLATE Latin1_General_100_CI_AS_KS_WS, [SalesTerritoryGroup] NVARCHAR(50) COLLATE Latin1_General_100_CI_AS_KS_WS NOT NULL, [col] BIGINT, [col1] MONEY NOT NULL, [col2] BIGINT, [col3] MONEY NOT NULL ) WITH(DATA_COMPRESSION=PAGE);</sql_operation>  
46        </sql_operations>  
47      </dsql_operation>  
48      <dsql_operation operation_type="SHUFFLE_MOVE">  
49        <operation_cost cost="0.804806144" accumulative_cost="0.926237696" average_rowsize="232" output_rows="108.406" />  
50        <source_statement>SELECT [T1_1].[StateProvinceName] AS [StateProvinceName],  
51         [T1_1].[SalesTerritoryGroup] AS [SalesTerritoryGroup],  
52         [T1_1].[col2] AS [col],  
53         [T1_1].[col] AS [col1],  
54         [T1_1].[col3] AS [col2],  
55         [T1_1].[col1] AS [col3]  
56  FROM   (SELECT ISNULL([T2_1].[col1], CONVERT (MONEY, 0.00, 0)) AS [col],  
57                 ISNULL([T2_1].[col3], CONVERT (MONEY, 0.00, 0)) AS [col1],  
58                 [T2_1].[StateProvinceName] AS [StateProvinceName],  
59                 [T2_1].[SalesTerritoryGroup] AS [SalesTerritoryGroup],  
60                 [T2_1].[col] AS [col2],  
61                 [T2_1].[col2] AS [col3]  
62          FROM   (SELECT   COUNT_BIG([T3_2].[YearlyIncome]) AS [col],  
63                           SUM([T3_2].[YearlyIncome]) AS [col1],  
64                           COUNT_BIG(CAST ((0) AS INT)) AS [col2],  
65                           SUM([T3_2].[SalesAmount]) AS [col3],  
66                           [T3_2].[StateProvinceName] AS [StateProvinceName],  
67                           [T3_1].[SalesTerritoryGroup] AS [SalesTerritoryGroup]  
68                  FROM     (SELECT [T4_1].[SalesTerritoryKey] AS [SalesTerritoryKey],  
69                                   [T4_1].[SalesTerritoryGroup] AS [SalesTerritoryGroup]  
70                            FROM   [AdventureWorksPDW2012].[dbo].[DimSalesTerritory] AS T4_1  
71                            WHERE  (([T4_1].[SalesTerritoryGroup] = CAST (N'North America' COLLATE Latin1_General_100_CI_AS_KS_WS AS NVARCHAR (13)) COLLATE Latin1_General_100_CI_AS_KS_WS)  
72                                    OR ([T4_1].[SalesTerritoryGroup] = CAST (N'Pacific' COLLATE Latin1_General_100_CI_AS_KS_WS AS NVARCHAR (7)) COLLATE Latin1_General_100_CI_AS_KS_WS))) AS T3_1  
73                           INNER JOIN  
74                           (SELECT [T4_1].[SalesTerritoryKey] AS [SalesTerritoryKey],  
75                                   [T4_2].[YearlyIncome] AS [YearlyIncome],  
76                                   [T4_2].[SalesAmount] AS [SalesAmount],  
77                                   [T4_1].[StateProvinceName] AS [StateProvinceName]  
78                            FROM   [AdventureWorksPDW2012].[dbo].[DimGeography] AS T4_1  
79                                   INNER JOIN  
80                                   (SELECT [T5_2].[GeographyKey] AS [GeographyKey],  
81                                           [T5_2].[YearlyIncome] AS [YearlyIncome],  
82                                           [T5_1].[SalesAmount] AS [SalesAmount]  
83                                    FROM   [AdventureWorksPDW2012].[dbo].[FactInternetSales] AS T5_1  
84                                           INNER JOIN  
85                                           [tempdb].[dbo].[TEMP_ID_16893] AS T5_2  
86                                           ON ([T5_1].[CustomerKey] = [T5_2].[CustomerKey])) AS T4_2  
87                                   ON ([T4_2].[GeographyKey] = [T4_1].[GeographyKey])) AS T3_2  
88                           ON ([T3_1].[SalesTerritoryKey] = [T3_2].[SalesTerritoryKey])  
89                  GROUP BY [T3_2].[StateProvinceName], [T3_1].[SalesTerritoryGroup]) AS T2_1) AS T1_1</source_statement>  
90        <destination_table>[TEMP_ID_16894]</destination_table>  
91        <shuffle_columns>StateProvinceName;</shuffle_columns>  
92      </dsql_operation>  
93      <dsql_operation operation_type="ON">  
94        <location permanent="false" distribution="AllComputeNodes" />  
95        <sql_operations>  
96          <sql_operation type="statement">DROP TABLE [tempdb].[dbo].[TEMP_ID_16893]</sql_operation>  
97        </sql_operations>  
98      </dsql_operation>  
99      <dsql_operation operation_type="RETURN">  
100        <location distribution="AllDistributions" />  
101        <select>SELECT   [T1_1].[col] AS [col],  
102           [T1_1].[col1] AS [col1],  
103           [T1_1].[StateProvinceName] AS [StateProvinceName],  
104           [T1_1].[SalesTerritoryGroup] AS [SalesTerritoryGroup],  
105           [T1_1].[col2] AS [col2]  
106  FROM     (SELECT CONVERT (INT, [T2_1].[col], 0) AS [col],  
107                   CONVERT (INT, [T2_1].[col1], 0) AS [col1],  
108                   [T2_1].[StateProvinceName] AS [StateProvinceName],  
109                   [T2_1].[SalesTerritoryGroup] AS [SalesTerritoryGroup],  
110                   [T2_1].[col] AS [col2]  
111            FROM   (SELECT CASE  
112                            WHEN ([T3_1].[col] = CAST ((0) AS BIGINT)) THEN CAST (NULL AS MONEY)  
113                            ELSE ([T3_1].[col1] / CONVERT (MONEY, [T3_1].[col], 0))  
114                           END AS [col],  
115                           CASE  
116                            WHEN ([T3_1].[col2] = CAST ((0) AS BIGINT)) THEN CAST (NULL AS MONEY)  
117                            ELSE ([T3_1].[col3] / CONVERT (MONEY, [T3_1].[col2], 0))  
118                           END AS [col1],  
119                           [T3_1].[StateProvinceName] AS [StateProvinceName],  
120                           [T3_1].[SalesTerritoryGroup] AS [SalesTerritoryGroup]  
121                    FROM   (SELECT ISNULL([T4_1].[col], CONVERT (BIGINT, 0, 0)) AS [col],  
122                                   ISNULL([T4_1].[col1], CONVERT (MONEY, 0.00, 0)) AS [col1],  
123                                   ISNULL([T4_1].[col2], CONVERT (BIGINT, 0, 0)) AS [col2],  
124                                   ISNULL([T4_1].[col3], CONVERT (MONEY, 0.00, 0)) AS [col3],  
125                                   [T4_1].[StateProvinceName] AS [StateProvinceName],  
126                                   [T4_1].[SalesTerritoryGroup] AS [SalesTerritoryGroup]  
127                            FROM   (SELECT   SUM([T5_1].[col]) AS [col],  
128                                             SUM([T5_1].[col1]) AS [col1],  
129                                             SUM([T5_1].[col2]) AS [col2],  
130                                             SUM([T5_1].[col3]) AS [col3],  
131                                             [T5_1].[StateProvinceName] AS [StateProvinceName],  
132                                             [T5_1].[SalesTerritoryGroup] AS [SalesTerritoryGroup]  
133                                    FROM     [tempdb].[dbo].[TEMP_ID_16894] AS T5_1  
134                                    GROUP BY [T5_1].[StateProvinceName], [T5_1].[SalesTerritoryGroup]) AS T4_1) AS T3_1) AS T2_1) AS T1_1  
135  ORDER BY [T1_1].[col2] DESC</select>  
136      </dsql_operation>  
137      <dsql_operation operation_type="ON">  
138        <location permanent="false" distribution="AllDistributions" />  
139        <sql_operations>  
140          <sql_operation type="statement">DROP TABLE [tempdb].[dbo].[TEMP_ID_16894]</sql_operation>  
141        </sql_operations>  
142      </dsql_operation>  
143    </dsql_operations>  
144  </dsql_query>  
  
```  
  
 **Significado de la salida de EXPLAIN**  
  
 La salida anterior contiene 144 líneas numeradas. Es posible que en su caso la salida de esta consulta difiera ligeramente. En la lista siguiente se describen las secciones importantes.  
  
-   En las líneas 3 a 16 se proporciona una descripción de la consulta que se está analizando.  
  
-   En la línea 17 se especifica que el número total de operaciones será 9. Puede buscar el inicio de cada operación si busca las palabras **dsql_operation**.  
  
-   En la línea 18 se inicia la operación 1. En las líneas 18 y 19 se indica que una operación **RND_ID** creará un número de id. aleatorio que se usará para la descripción de un objeto. El objeto que se describe en la salida anterior es **TEMP_ID_16893**. Su número será diferente.  
  
-   En la línea 20 se inicia la operación 2. Líneas 21 a 25: en todos los nodos de ejecución se crea una tabla temporal denominada **TEMP_ID_16893**.  
  
-   En la línea 26 se inicia la operación 3. Líneas 27 a 37: los datos se mueven a **TEMP_ID_16893** mediante un movimiento de difusión. Se proporciona la consulta enviada a cada nodo de ejecución. En la línea 37 se especifica que la tabla de destino es **TEMP_ID_16893**.  
  
-   En la línea 38 se inicia la operación 4. Líneas 39 a 40: se crea un identificador aleatorio para una tabla. En el ejemplo anterior, el número de id. es **TEMP_ID_16894**. Su número será diferente.  
  
-   En la línea 41 se inicia la operación 5. Líneas 42 a 46: en todos los nodos, se crea una tabla temporal denominada **TEMP_ID_16894**.  
  
-   En la línea 47 se inicia la operación 6. Líneas 48 a 91: los datos de varias tablas (incluida **TEMP_ID_16893**) se mueven a la tabla **TEMP_ID_16894**, mediante una operación de movimiento aleatorio. Se proporciona la consulta enviada a cada nodo de ejecución. En la línea 90 se especifica que la tabla de destino es **TEMP_ID_16894**. En la línea 91 se especifican las columnas.  
  
-   En la línea 92 se inicia la operación 7. Líneas 93 a 97: en todos los nodos de ejecución se elimina la tabla temporal **TEMP_ID_16893**.  
  
-   En la línea 98 se inicia la operación 8. Líneas 99 a 135: los resultados se devuelven al cliente. Se usa la consulta proporcionada para obtener los resultados.  
  
-   En la línea 136 se inicia la operación 9. Líneas 137 a 140: en todos los nodos, se elimina la tabla temporal **TEMP_ID_16894**.  
  
  

