---
title: EXPLICAR (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 08/09/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|queries
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4846a576-57ea-4068-959c-81e69e39ddc1
caps.latest.revision: "13"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 3aa20ea08fe34eab316a41d46ea955a78e4be512
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="explain-transact-sql"></a>EXPLICAR (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Devuelve el plan de consulta para un [!INCLUDE[ssDW](../../includes/ssdw-md.md)] [!INCLUDE[DWsql](../../includes/dwsql-md.md)] instrucción sin ejecutar la instrucción. Use **EXPLICATIVO** para vista previa de las operaciones que requerirá el movimiento de datos y ver los costos estimados de las operaciones de consulta.  
  
 Para obtener más información acerca de los planes de consulta, vea "Descripción planes de consulta" en la [!INCLUDE[pdw-product-documentation_md](../../includes/pdw-product-documentation-md.md)].  
  
## <a name="syntax"></a>Sintaxis  
  

```  
EXPLAIN SQL_statement  
[;]  
```  
  
## <a name="arguments"></a>Argumentos  
 *SQL_statement*  
 El [!INCLUDE[DWsql](../../includes/dwsql-md.md)] instrucción en el que **EXPLICATIVO** se ejecutará. *SQL_statement* puede ser cualquiera de estos comandos: **seleccione**, **insertar**, **actualización**, **eliminar**,  **Crear tabla como SELECT**, **crear una tabla remota**.  
  
## <a name="permissions"></a>Permissions  
 Requiere la **SHOWPLAN** permiso y el permiso para ejecutar *SQL_statement*. Vea [permisos: GRANT, DENY, REVOKE &#40; Almacenamiento de datos SQL Azure, almacenamiento de datos en paralelo &#41; ](../../t-sql/statements/permissions-grant-deny-revoke-azure-sql-data-warehouse-parallel-data-warehouse.md).  
  
## <a name="return-value"></a>Valor devuelto  
 El valor devuelto de la **EXPLICATIVO** comando es un documento XML con la estructura que se muestra a continuación. Este documento XML enumeran todas las operaciones en el plan de consulta en la consulta especificada, cada uno de ellos delimitadas por la `<dsql_operation>` etiqueta. El valor devuelto es de tipo **nvarchar (max)**.  
  
 El plan de consulta devuelta representa sentencias SQL secuenciales; Cuando se ejecuta la consulta puede implicar las operaciones de ejecución en paralelo, por lo que algunas de las instrucciones secuenciales que se muestra pueden ejecutar al mismo tiempo.  
  
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
  
|(Etiqueta XML)|Resumen, atributos y contenido|  
|-------------|--------------------------------------|  
|\<dsql_query >|Elemento de documento o de nivel superior.|
|\<SQL >|Devuelve como eco *SQL_statement*.|  
|\<params >|Esta etiqueta no se utiliza en este momento.|  
|\<dsql_operations >|Se resumen y contiene los pasos de consulta e incluye información de costo de la consulta. También contiene todos los `<dsql_operation>` bloques. Esta etiqueta contiene información de recuento para toda la consulta:<br /><br /> `<dsql_operations total_cost=total_cost total_number_operations=total_number_operations>`<br /><br /> *total_cost* es el tiempo total estimado para la consulta se ejecute, en milisegundos.<br /><br /> *total_number_operations* es el número total de operaciones para la consulta. Una operación que se pueden ejecutar en paralelo y ejecutar en varios nodos se cuenta como una única operación.|  
|\<dsql_operation >|Describe una operación única dentro del plan de consulta. El \<dsql_operation > etiqueta contiene el tipo de operación como un atributo:<br /><br /> `<dsql_operation operation_type=operation_type>`<br /><br /> *operation_type* es uno de los valores encontrados en [consulta de datos (SQL Server PDW)](http://msdn.microsoft.com/en-us/3f4f5643-012a-4c36-b5ec-691c4bbe668c).<br /><br /> El contenido de la `\<dsql_operation>` bloque es depende del tipo de operación.<br /><br /> Vea la siguiente tabla.|  
  
|Tipo de operación|Contenido|Ejemplo|  
|--------------------|-------------|-------------|  
|BROADCAST_MOVE, DISTRIBUTE_REPLICATED_TABLE_MOVE, MASTER_TABLE_MOVE, PARTITION_MOVE, SHUFFLE_MOVE y TRIM_MOVE|`<operation_cost>`elemento, con estos atributos. Valores reflejan sólo la operación local:<br /><br /> -   *costo* es el costo de operador local y muestra el tiempo estimado para la operación que se ejecuta, en milisegundos.<br />-   *accumulative_cost* es la suma de todas las operaciones encontradas en el plan incluye valores de la suma de las operaciones paralelas, en milisegundos.<br />-   *average_rowsize* es el tamaño de fila medio estimado (en bytes) de filas recuperado y pasa durante la operación.<br />-   *output_rows* es la cardinalidad de salida (nodo) y muestra el número de filas de salida.<br /><br /> `<location>`: Los nodos o las distribuciones que se realizará la operación. Opciones son: "Control", "ComputeNode", "AllComputeNodes", "AllDistributions", "SubsetDistributions", "Distribución" y "SubsetNodes".<br /><br /> `<source_statement>`: Mover los datos de origen para el orden aleatorio.<br /><br /> `<destination_table>`: La tabla temporal interna se moverán los datos a.<br /><br /> `<shuffle_columns>`: (Aplicable solo a las operaciones de SHUFFLE_MOVE). Una o varias columnas que se usará como las columnas de distribución para la tabla temporal.|`<operation_cost cost="40" accumulative_cost="40" average_rowsize = "50" output_rows="100"/>`<br /><br /> `<location distribution="AllDistributions" />`<br /><br /> `<source_statement type="statement">SELECT [TableAlias_3b77ee1d8ccf4a94ba644118b355db9d].[dist_date] FROM [qatest].[dbo].[flyers] [TableAlias_3b77ee1d8ccf4a94ba644118b355db9d]       </source_statement>`<br /><br /> `<destination_table>Q_[TEMP_ID_259]_[PARTITION_ID]</destination_table>`<br /><br /> `<shuffle_columns>dist_date;</shuffle_columns>`|  
|CopyOperation|`<operation_cost>`: Permite ver `<operation_cost>` anteriormente.<br /><br /> `<DestinationCatalog>`: El nodo de destino o los nodos.<br /><br /> `<DestinationSchema>`: El esquema de destino en DestinationCatalog.<br /><br /> `<DestinationTableName>`: Nombre de la tabla de destino o "TableName".<br /><br /> `<DestinationDatasource>`: La información de conexión o el nombre del origen de datos de destino.<br /><br /> `<Username>`y `<Password>`: estos campos indican que un nombre de usuario y una contraseña para el destino pueden ser necesarios.<br /><br /> `<BatchSize>`: El tamaño de lote para la operación de copia.<br /><br /> `<SelectStatement>`: La instrucción select utilizada para realizar la copia.<br /><br /> `<distribution>`: La distribución donde se realiza la copia.|`<operation_cost cost="0" accumulative_cost="0" average_rowsize="4" output_rows="1" />`<br /><br /> `<DestinationCatalog>master</DestinationCatalog>`<br /><br /> `<DestinationSchema>dbo</DestinationSchema>`<br /><br /> `<DestinationTableName>[TableName]</DestinationTableName>`<br /><br /> `<DestinationDatasource>localhost, 8080</DestinationDatasource>`<br /><br /> `<Username>...</Username>`<br /><br /> `<Password>...</Password>`<br /><br /> `<BatchSize>6000</BatchSize>`<br /><br /> `<SelectStatement>SELECT T1_1.c1 AS c1 FROM [qatest].[dbo].[gigs] AS T1_1</SelectStatement>`<br /><br /> `<distribution>ControlNode</distribution>`|  
|MetaDataCreate_Operation|`<source_table>`: La tabla de origen para la operación.<br /><br /> `<destionation_table>`: La tabla de destino para la operación.|`<source_table>databases</source_table>`<br /><br /> `<destination_table>MetaDataCreateLandingTempTable</destination_table>`|  
|ON|`<location>`: Permite ver `<location>` anteriormente.<br /><br /> `<sql_operation>`: Identifica el comando SQL que se realizarán en un nodo.|`<location permanent="false" distribution="AllDistributions">Compute</location>`<br /><br /> `<sql_operation type="statement">CREATE TABLE [tempdb].[dbo]. [Q_[TEMP_ID_259]]_ [PARTITION_ID]]]([dist_date] DATE) WITH (DISTRIBUTION = HASH([dist_date]),) </sql_operation>`|  
|RemoteOnOperation|`<DestinationCatalog>`: El catálogo de destino.<br /><br /> `<DestinationSchema>`: El esquema de destino en DestinationCatalog.<br /><br /> `<DestinationTableName>`: Nombre de la tabla de destino o "TableName".<br /><br /> `<DestinationDatasource>`: Nombre del origen de datos de destino.<br /><br /> `<Username>`y `<Password>`: estos campos indican que un nombre de usuario y una contraseña para el destino pueden ser necesarios.<br /><br /> `<CreateStatement>`: La instrucción de creación de tabla para la base de datos de destino.|`<DestinationCatalog>master</DestinationCatalog>`<br /><br /> `<DestinationSchema>dbo</DestinationSchema>`<br /><br /> `<DestinationTableName>TableName</DestinationTableName>`<br /><br /> `<DestinationDatasource>DestDataSource</DestinationDatasource>`<br /><br /> `<Username>...</Username>`<br /><br /> `<Password>...</Password>`<br /><br /> `<CreateStatement>CREATE TABLE [master].[dbo].[TableName] ([col1] BIGINT) ON [PRIMARY] WITH(DATA_COMPRESSION=PAGE);</CreateStatement>`|  
|RETURN|`<resultset>`: El identificador del conjunto de resultados.|`<resultset>RS_19</resultset>`|  
|RND_ID|`<identifier>`: El identificador del objeto creado.|`<identifier>TEMP_ID_260</identifier>`|  
  
## <a name="limitations-and-restrictions"></a>Limitaciones y restricciones  
 **EXPLICA** puede aplicarse a *optimizables* según los resultados de las consultas, que son consultas que se pueden mejorar o modificar un **EXPLICAN** comando. Admiten **EXPLICATIVO** comandos son mencionados anteriormente. Cualquier intento de usar **EXPLICATIVO** con una consulta no admitida tipo se devolverá un error o la consulta de eco.  
  
 **EXPLIQUE** no se admite en una transacción de usuario.  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente muestra un **EXPLICATIVO** comando ejecutarse en un **seleccione** instrucción y el resultado XML.  
  
 **Envía una instrucción de explicación**  
  
 El comando enviado por este ejemplo es:  
  
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
  
 Después de ejecutar la instrucción mediante la **EXPLICATIVO** opción, la pestaña mensaje presenta una sola línea titulada **explican**e iniciar con el texto XML `\<?xml version="1.0" encoding="utf-8"?>` haga clic en el código XML para abrir todo el texto en un Ventana XML. Para entender mejor los comentarios siguientes, debe activar la presentación de números de línea en SSDT.  
  
#### <a name="to-turn-on-line-numbers"></a>Para activar los números de línea  
  
1.  Con el resultado que aparece en el **explican** ficha SSDT, la **herramientas** menú, seleccione **opciones**.  
  
2.  Expanda el **Editor de texto** sección, expanda **XML**y, a continuación, haga clic en **General**.  
  
3.  En el **mostrar** área, verificación **números de línea**.  
  
4.  Haga clic en **Aceptar**.  
  
 **Resultado del ejemplo explicación**  
  
 El resultado XML de la **EXPLICATIVO** comando con los números de fila activados es:  
  
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
  
 **Significado de la salida de explicación**  
  
 La salida anterior contiene 144 líneas numeradas. El resultado de esta consulta puede diferir ligeramente. La siguiente lista describe las secciones importantes.  
  
-   Líneas de 3 a 16 proporcionan una descripción de la consulta que se está analizando.  
  
-   Línea 17, especifica que el número total de operaciones será 9. Puede buscar el inicio de cada operación, buscando las palabras **dsql_operation**.  
  
-   La línea 18 inicia la operación 1. Líneas 18 y 19 indican que un **RND_ID** operación creará un número de identificador aleatorio que se usará para una descripción del objeto. El objeto que se describe en la salida anterior es **TEMP_ID_16893**. El número será diferente.  
  
-   Línea 20 inicia la operación 2. Líneas de 21 a 25: en todos los nodos de proceso, cree una tabla temporal denominada **TEMP_ID_16893**.  
  
-   Línea 26 inicia la operación 3. Líneas 27 a través de 37: mover los datos **TEMP_ID_16893** mediante el uso de un movimiento de difusión. Se proporciona la consulta enviada a cada nodo de proceso. Línea 37 especifica la tabla de destino es **TEMP_ID_16893**.  
  
-   Línea 38 inicia la operación de 4. Líneas 39 a 40: crear un identificador aleatorio para una tabla. **TEMP_ID_16894** es el número de identificación en el ejemplo anterior. El número será diferente.  
  
-   Línea 41 inicia la operación 5. Líneas 42 a través de 46: en todos los nodos, cree una tabla temporal denominada **TEMP_ID_16894**.  
  
-   Línea 47 inicia la operación de 6. Líneas 48 al 91: mover los datos de varias tablas (incluidos **TEMP_ID_16893**) a la tabla **TEMP_ID_16894**, mediante el uso de un orden aleatorio de operación de movimiento. Se proporciona la consulta enviada a cada nodo de proceso. Línea 90 especifica la tabla de destino como **TEMP_ID_16894**. Línea 91 especifica las columnas.  
  
-   Línea 92 inicia la operación de 7. Líneas 93 a través de 97: en todos los nodos de proceso, coloque la tabla temporal **TEMP_ID_16893**.  
  
-   Línea 98 inicia la operación de 8. Líneas 99 a través de 135: devolver resultados al cliente. Usa la consulta proporcionada para obtener los resultados.  
  
-   Línea 136 inicia la operación de 9. Líneas 137, hasta 140: en todos los nodos, quitar tabla temporal **TEMP_ID_16894**.  
  
  

