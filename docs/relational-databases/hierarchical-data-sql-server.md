---
description: Datos jerárquicos (SQL Server)
title: Datos jerárquicos (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 10/04/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- hierarchies [SQL Server], tables to support
- hierarchyid [Database Engine], concepts
- hierarchical tables [Database Engine]
- SqlHierarchyId
- hierarchyid [Database Engine]
- hierarchical queries [SQL Server], using hierarchyid data type
ms.assetid: 19aefa9a-fbc2-4b22-92cf-67b8bb01671c
author: rothja
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 994adada7ecef047967b07d03cd2a9a129c8f227
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/09/2020
ms.locfileid: "91869053"
---
# <a name="hierarchical-data-sql-server"></a>Datos jerárquicos (SQL Server)

[!INCLUDE [SQL Server Azure SQL Database](../includes/applies-to-version/sql-asdb.md)]

  El tipo de datos **hierarchyid** integrado facilita el almacenamiento y la consulta de datos jerárquicos. **hierarchyid** se optimiza para representar los árboles, que son el tipo más común de datos jerárquicos.  
  
 Los datos jerárquicos se definen como un conjunto de elementos de datos que se relacionan entre sí mediante relaciones jerárquicas. Las relaciones jerárquicas existen allí donde un elemento de los datos es el elemento primario de otro elemento. Entre los ejemplos de datos jerárquicos que se almacenan normalmente en las bases de datos se incluyen los siguientes:  
  
-   Una estructura organizativa  
  
-   Un sistema de archivos  
  
-   Un conjunto de tareas de un proyecto  
  
-   Una taxonomía de términos de idioma  
  
-   Un gráfico de vínculos entre páginas web  
  
 Use [hierarchyid](../t-sql/data-types/hierarchyid-data-type-method-reference.md) como tipo de datos para crear tablas con una estructura jerárquica o para describir la estructura jerárquica de datos almacenados en otra ubicación. Use las [funciones hierarchyid](../t-sql/data-types/hierarchyid-data-type-method-reference.md) de [!INCLUDE[tsql](../includes/tsql-md.md)] para consultar y administrar los datos jerárquicos.  
  
##  <a name="key-properties-of-hierarchyid"></a><a name="keyprops"></a> Propiedades principales de hierarchyid  
 Un valor del tipo de datos **hierarchyid** representa una posición en una jerarquía de árbol. Los valores de **hierarchyid** tienen las siguientes propiedades.  
  
-   Muy compactos  
  
     El número medio de bits necesarios para representar un nodo en un árbol con *n* nodos depende del promedio de distribución ramificada secundarios (el promedio de elementos secundarios de un nodo). Para distribuciones ramificadas pequeñas (0-7), el tamaño es aproximadamente 6\*logA*n* bits, donde A es el promedio de distribución ramificada. Un nodo en una jerarquía organizativa de 100.000 personas con un promedio de nodos secundarios de 6 niveles supone aproximadamente 38 bits. Esto se redondea a 40 bits (o 5 bytes) para el almacenamiento.  
  
-   La comparación se realiza con prioridad a la profundidad  
  
     Dados dos valores **hierarchyid****a** y **b**, **a<b** significa que a viene antes que b en un corte transversal de prioridad a la profundidad del árbol. Los índices de los tipos de datos **hierarchyid** están en orden con prioridad a la profundidad y los nodos cercanos entre sí en un corte transversal de prioridad a la profundidad se almacenan casi uno junto a otro. Por ejemplo, los elementos secundarios de un registro se almacenan adyacentes a ese registro.  
  
-   Compatibilidad con inserciones y eliminaciones arbitrarias  
  
     Con el método [GetDescendant](../t-sql/data-types/getdescendant-database-engine.md) siempre es posible generar un miembro del mismo nivel a la derecha de cualquier nodo determinado, a la izquierda de cualquier nodo determinado, o entre dos miembros cualesquiera del mismo nivel. Se mantiene la propiedad comparison cuando se inserta o elimina un número arbitrario de nodos de la jerarquía. La mayoría de las inserciones y eliminaciones conservan la propiedad compactness. Sin embargo, las inserciones entre dos nodos generarán valores hierarchyid con una representación ligeramente menos compacta.  
  
  
##  <a name="limitations-of-hierarchyid"></a><a name="limits"></a> Limitaciones de hierarchyid  
 El tipo de datos **hierarchyid** tiene las siguientes limitaciones:  
  
-   Una columna de tipo **hierarchyid** no representa automáticamente un árbol. Dependerá de la aplicación generar y asignar los valores **hierarchyid** de tal forma que la relación deseada entre las filas se refleje en los valores. Algunas aplicaciones pueden tener una columna de tipo **hierarchyid** que indica la ubicación en una jerarquía definida en otra tabla.  
  
-   Depende de la aplicación el administrar la simultaneidad en la generación y asignación de valores **hierarchyid** . No hay ninguna garantía de que los valores **hierarchyid** de una columna sean únicos, a menos que la aplicación use una restricción de clave única o se aplique singularidad a través de su lógica.  
  
-   Las relaciones jerárquicas representadas por valores **hierarchyid** no se aplican como una relación de clave externa. Es posible, y a veces adecuado, establecer una relación jerárquica donde A tiene un elemento secundario B, de forma que A se elimina dejando a B con una relación con un registro no existente. Si este comportamiento no es aceptable, la aplicación debe consultar a los descendientes antes de eliminar los miembros primarios.  
  
  
##  <a name="when-to-use-alternatives-to-hierarchyid"></a><a name="alternatives"></a> Cuándo utilizar alternativas a hierarchyid  
 Dos alternativas a **hierarchyid** para representar los datos jerárquicos son:  
  
-   Elemento primario/secundario  
  
-   XML  
  
 Normalmente,**hierarchyid** es mejor opción en comparación con estas alternativas. Sin embargo, hay situaciones concretas, que se detallan a continuación, donde es probable que las alternativas sean una mejor opción.  
  
### <a name="parentchild"></a>Elemento primario/secundario  
 Cuando se usa el planteamiento de elemento primario/secundario, cada fila contiene una referencia al elemento primario. La tabla siguiente define una tabla típica que se usa para contener las filas del elemento primario y el secundario en una relación entre elemento primario y secundario:  
  
```sql
USE AdventureWorks2012 ;  
GO  
  
CREATE TABLE ParentChildOrg  
   (  
    BusinessEntityID int PRIMARY KEY,  
    ManagerId int REFERENCES ParentChildOrg(BusinessEntityID),  
    EmployeeName nvarchar(50)   
   ) ;  
GO  
```  
  
 Comparar el elemento primario/secundario y **hierarchyid** en operaciones comunes  
  
-   Las consultas de subárboles son significativamente más rápidas con **hierarchyid**.  
  
-   Las consultas directas de descendientes son ligeramente más lentas con **hierarchyid**.  
  
-   Mover los nodos no hoja es más lento con **hierarchyid**.  
  
-   Insertar nodos no hoja e insertar o mover nodos hoja es igual de complejo con **hierarchyid**.  
  
 La estructura de elemento primario/secundario puede ser mejor opción cuando se dan las condiciones siguientes:  
  
-   El tamaño de la clave es crítico. Para el mismo número de nodos, un valor **hierarchyid** es igual o mayor que un valor de la familia de enteros (**smallint**, **int**, **bigint**). Esta es solo una de las razones para usar la estructura de elemento primario/secundario en casos poco comunes, ya que **hierarchyid** tiene una proximidad significativamente mejor de E/S y de complejidad de la CPU que las expresiones de tabla comunes necesarias cuando se usa una estructura de elemento primario/secundario.  
  
-   Las consultas raramente recorren todas las secciones de la jerarquía. Dicho de otro modo, las consultas normalmente se dirigen a un solo punto de la jerarquía. En estos casos la ubicación conjunta no es importante. Por ejemplo, la estructura de elemento primario y secundario es la mejor opción cuando la tabla de organización solo se usa para procesar la nómina de empleados individuales.  
  
-   Los subárboles no hoja se mueven con frecuencia y el rendimiento es muy importante. En una representación de elemento primario/secundario, el cambio de ubicación de una fila en una jerarquía afecta a una única fila. Si se cambia la ubicación de una fila cuando se usa **hierarchyid** , ello afectará a *n* filas, donde *n* es el número de nodos de un subárbol que se están moviendo.  
  
     Si los subárboles no hoja se mueven con frecuencia y el rendimiento es importante, pero la mayoría de los movimientos se encuentran en un nivel bien definido de la jerarquía, tenga en cuenta la posibilidad de dividir los niveles más altos y más bajos en dos jerarquías. Esto convierte todos los movimientos en niveles de hoja de la jerarquía más alta. Por ejemplo, considere la posibilidad de tener una jerarquía de sitios web hospedada por un servicio. Los sitios contienen muchas páginas organizadas de forma jerárquica. Los sitios hospedados se pueden mover a otras ubicaciones en la jerarquía del sitio, pero las páginas subordinadas rara vez se reorganizan. Esto se podría representar mediante:  
  
    ```sql
    CREATE TABLE HostedSites   
       (  
        SiteId hierarchyid, PageId hierarchyid  
       ) ;  
    GO  
    ```  
  
  
### <a name="xml"></a>XML  
 Un documento XML es un árbol y, por lo tanto, una única instancia de tipo de datos XML puede representar una jerarquía completa. In [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] when an XML dedex is created, **hierarchyid** values are used deternally to represent the position de the hierarchy.  
  
 Utilizar el tipo de datos XML puede ser mejor opción cuando se cumplen todas las condiciones siguientes:  
  
-   Siempre se almacena y se recupera la jerarquía completa.  
  
-   La aplicación consume los datos en formato XML.  
  
-   Las búsquedas del predicado están muy limitadas y no son vitales para el rendimiento.  
  
 Por ejemplo, cuando una aplicación realiza el seguimiento de varias organizaciones, siempre almacena y recupera la jerarquía de la organización completa y no consulta en una sola organización, entonces podría tener sentido utilizar una tabla con la forma siguiente:  
  
```sql
CREATE TABLE XMLOrg   
    (  
    Orgid int,  
    Orgdata xml  
    ) ;  
GO  
```  
  
  
##  <a name="indexing-strategies-for-hierarchical-data"></a><a name="indexing"></a> Estrategias de indización para los datos jerárquicos  
 Hay dos estrategias para indizar datos jerárquicos:  
  
-   **Con prioridad a la profundidad**  
  
     En un índice con prioridad de profundidad, las filas de un subárbol se almacenan unas junto a otras. Por ejemplo, todos los empleados al mando de un gerente se almacenan junto al registro de este último.  
  
     En un índice con prioridad de profundidad, todos los nodos del subárbol de un nodo se ubican conjuntamente. Por lo tanto, los índices con prioridad a la profundidad son eficaces para responder a las consultas sobre subárboles, como "Buscar todos los archivos en esta carpeta y en sus subcarpetas".  
  
-   **Con prioridad a la amplitud**  
  
     Un índice con prioridad a la amplitud almacena juntas las filas de cada nivel de la jerarquía. Por ejemplo, se almacenan unos junto a otros los registros de empleados que notifican directamente al mismo gerente.  
  
     En un índice con prioridad a la amplitud, todos los elementos secundarios directos de un nodo se ubican conjuntamente. Por lo tanto, los índices con prioridad a la amplitud son eficaces para responder a las consultas sobre elementos secundarios inmediatos, como "Buscar todos los empleados que informan directamente a este gerente".  
  
 Saber si es mejor tener un índice con prioridad de profundidad, con prioridad de amplitud, o ambos, y cuál de estos se debe establecer como clave de agrupación en clústeres (cuando proceda), depende de la importancia relativa de los tipos de consultas anteriores y de la importancia relativa de las operaciones SELECT frente a las de DML. Para obtener un ejemplo detallado de las estrategias de indización, consulte [Tutorial: Using the hierarchyid Data Type](../relational-databases/tables/tutorial-using-the-hierarchyid-data-type.md).  
  
  
### <a name="creating-indexes"></a>Crear índices  
 El método GetLevel() se puede usar para crear una ordenación con prioridad a la amplitud. En el ejemplo siguiente se han creado los índices con prioridad a la amplitud y con prioridad a la profundidad:  
  
```sql
USE AdventureWorks2012 ;   -- wmimof
GO  
  
CREATE TABLE Organization  
   (  
    BusinessEntityID hierarchyid,  
    OrgLevel as BusinessEntityID.GetLevel(),   
    EmployeeName nvarchar(50) NOT NULL  
   ) ;  
GO  
  
CREATE CLUSTERED INDEX Org_Breadth_First   
    ON Organization(OrgLevel,BusinessEntityID) ;  
GO  
  
CREATE UNIQUE INDEX Org_Depth_First   
    ON Organization(BusinessEntityID) ;  
GO  
```  
  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="simple-example"></a>Ejemplo sencillo  
 El ejemplo siguiente es deliberadamente simplista para ayudarle a empezar. Cree primero una tabla que contenga algunos datos de geografía.  
  
```sql
CREATE TABLE SimpleDemo  
(
    Level hierarchyid NOT NULL,  
    Location nvarchar(30) NOT NULL,  
    LocationType nvarchar(9) NULL
);
```  
  
 Ahora inserte datos para algunos continentes, países, estados y ciudades.  
  
```sql
INSERT SimpleDemo  
    VALUES   
('/1/', 'Europe', 'Continent'),  
('/2/', 'South America', 'Continent'),  
('/1/1/', 'France', 'Country'),  
('/1/1/1/', 'Paris', 'City'),  
('/1/2/1/', 'Madrid', 'City'),  
('/1/2/', 'Spain', 'Country'),  
('/3/', 'Antarctica', 'Continent'),  
('/2/1/', 'Brazil', 'Country'),  
('/2/1/1/', 'Brasilia', 'City'),  
('/2/1/2/', 'Bahia', 'State'),  
('/2/1/2/1/', 'Salvador', 'City'),  
('/3/1/', 'McMurdo Station', 'City');  
```  
  
 Seleccione los datos, agregando una columna que convierta los datos de nivel a un valor de texto que sea fácil de entender. Esta consulta también ordena el resultado por el tipo de datos **hierarchyid** .  
  
```sql
SELECT CAST(Level AS nvarchar(100)) AS [Converted Level], *   
    FROM SimpleDemo ORDER BY Level;  
```  
  
 [!INCLUDE[ssResult](../includes/ssresult-md.md)]  
  
```  
Converted Level  Level     Location         LocationType  
/1/              0x58      Europe           Continent  
/1/1/            0x5AC0    France           Country  
/1/1/1/          0x5AD6    Paris            City  
/1/2/            0x5B40    Spain            Country  
/1/2/1/          0x5B56    Madrid           City  
/2/              0x68      South America    Continent  
/2/1/            0x6AC0    Brazil           Country  
/2/1/1/          0x6AD6    Brasilia         City  
/2/1/2/          0x6ADA    Bahia            State  
/2/1/2/1/        0x6ADAB0  Salvador         City  
/3/              0x78      Antarctica       Continent  
/3/1/            0x7AC0    McMurdo Station  City  
```  
  
 Observe que la jerarquía tiene una estructura válida, aunque no sea coherente internamente. Bahia es el único estado. Aparece en la jerarquía como un homólogo de la ciudad Brasilia. Del mismo modo, McMurdo Station no tiene un país primario. Los usuarios deben decidir si este tipo de jerarquía es adecuado para su uso.  
  
 Agregue otra fila y seleccione los resultados.  
  
```sql
INSERT SimpleDemo  
    VALUES ('/1/3/1/', 'Kyoto', 'City'), ('/1/3/1/', 'London', 'City');  
SELECT CAST(Level AS nvarchar(100)) AS [Converted Level], * FROM SimpleDemo ORDER BY Level;  
```  
  
 Esto muestra más problemas posibles. Kyoto se puede insertar como el nivel `/1/3/1/` aunque no hay ningún nivel primario `/1/3/`. Y tanto London como Kyoto tienen el mismo valor de **hierarchyid**. Una vez más, los usuarios deben decidir si este tipo de jerarquía es adecuado para su uso y bloquear los valores que no se puedan usar.  
  
 Además, en esta tabla no se usó la parte superior de la jerarquía `'/'`. Se omitió porque no hay ningún elemento primario común de todos los continentes. Puede agregar uno si agrega todo el planeta.  
  
```sql
INSERT SimpleDemo  
    VALUES ('/', 'Earth', 'Planet');  
```  
  
##  <a name="related-tasks"></a><a name="tasks"></a> Tareas relacionadas  
  
###  <a name="migrating-from-parentchild-to-hierarchyid"></a><a name="migrating"></a> Migrar de elemento primario/secundario a hierarchyid  
 La mayoría de los árboles se representan mediante elementos primario y secundario. La manera más fácil de migrar de una estructura de elemento primario y secundario a una tabla que use **hierarchyid** consiste en usar una columna temporal o una tabla temporal para realizar el seguimiento del número de nodos en cada nivel de la jerarquía. Para ver un ejemplo sobre la migración de una tabla de elemento primario/secundario, consulte la lección 1 de [Tutorial: Usar el tipo de datos hierarchyid](../relational-databases/tables/tutorial-using-the-hierarchyid-data-type.md).  
  
  
###  <a name="managing-a-tree-using-hierarchyid"></a><a name="BKMK_ManagingTrees"></a> Administrar un árbol mediante hierarchyid  
 Aunque una columna de **hierarchyid** no representa necesariamente un árbol, una aplicación puede exigir fácilmente que sí lo haga.  
  
-   Cuando genere nuevos valores, realice una de las siguientes operaciones:  
  
    -   Realice el seguimiento del último número secundario en la fila primaria.  
  
    -   Calcule el último elemento secundario. Si desea realizar eficazmente este proceso, deberá ejecutar un índice con prioridad a la amplitud.  
  
-   Exija la singularidad creando un índice único en la columna, tal vez como parte de una clave de agrupación en clústeres. Para asegurarse de que se insertan valores únicos, realice una de las siguientes tareas:  
  
    -   Detecte errores y reintentos de infracción de clave única.  
  
    -   Determine la singularidad de cada nuevo nodo secundario e insértelo como parte de una transacción serializable.  
  
  
#### <a name="example-using-error-detection"></a>Ejemplo usando la detección de errores  
 En el ejemplo siguiente, el código de ejemplo calcula el nuevo valor secundario de **EmployeeId** y, después, detecta cualquier infracción de clave y la devuelve al marcador **INS_EMP** para volver a calcular el valor de **EmployeeId** para la nueva fila:  
  
```sql
USE AdventureWorks ;  
GO  
  
CREATE TABLE Org_T1  
   (  
    EmployeeId hierarchyid PRIMARY KEY,  
    OrgLevel AS EmployeeId.GetLevel(),  
    EmployeeName nvarchar(50)   
   ) ;  
GO  
  
CREATE INDEX Org_BreadthFirst ON Org_T1(OrgLevel, EmployeeId);
GO  
  
CREATE PROCEDURE AddEmp(@mgrid hierarchyid, @EmpName nvarchar(50) )   
AS  
BEGIN  
    DECLARE @last_child hierarchyid;
INS_EMP:   
    SELECT @last_child = MAX(EmployeeId) FROM Org_T1   
        WHERE EmployeeId.GetAncestor(1) = @mgrid;
    INSERT INTO Org_T1 (EmployeeId, EmployeeName)  
        SELECT @mgrid.GetDescendant(@last_child, NULL), @EmpName;
-- On error, return to INS_EMP to recompute @last_child  
IF @@error <> 0 GOTO INS_EMP   
END ;  
GO  
```  
  
  
#### <a name="example-using-a-serializable-transaction"></a>Ejemplo usando una transacción serializable  
 El índice **Org_BreadthFirst** garantiza que se use una búsqueda de rango al determinar **\@last_child**. Además de otros casos de error, es posible que una aplicación quiera comprobar una infracción de clave duplicada después de que la inserción indique un intento de agregar varios empleados con el mismo identificador y, por lo tanto, sea necesario volver a calcular **\@last_child**. En el código siguiente se calcula el nuevo valor de nodo dentro de una transacción serializable:  
  
```sql
CREATE TABLE Org_T2  
    (  
    EmployeeId hierarchyid PRIMARY KEY,  
    LastChild hierarchyid,   
    EmployeeName nvarchar(50)   
    ) ;  
GO  
  
CREATE PROCEDURE AddEmp(@mgrid hierarchyid, @EmpName nvarchar(50))   
AS  
BEGIN  
DECLARE @last_child hierarchyid  
SET TRANSACTION ISOLATION LEVEL SERIALIZABLE  
BEGIN TRANSACTION   
  
SELECT @last_child  =  EmployeeId.GetDescendant(LastChild,NULL)
FROM Org_T2
WHERE EmployeeId = @mgrid

UPDATE Org_T2 SET LastChild = @last_child  WHERE EmployeeId = @mgrid

INSERT Org_T2 (EmployeeId, EmployeeName)   
    VALUES(@last_child, @EmpName)  
COMMIT  
END ;  
```  
  
 El código siguiente rellena la tabla con tres filas y devuelve los resultados:  
  
```sql
INSERT Org_T2 (EmployeeId, EmployeeName)   
    VALUES(hierarchyid::GetRoot(), 'David') ;  
GO  
AddEmp 0x , 'Sariya'  
GO  
AddEmp 0x58 , 'Mary'  
GO  
SELECT * FROM Org_T2  
```  
  
 [!INCLUDE[ssResult](../includes/ssresult-md.md)]  
  
```  
EmployeeId LastChild EmployeeName  
---------- --------- ------------  
0x        0x58       David  
0x58      0x5AC0     Sariya  
0x5AC0    NULL       Mary  
```  
  
  
###  <a name="enforcing-a-tree"></a><a name="BKMK_EnforcingTrees"></a> Exigir un árbol  
 Los ejemplos anteriores muestran cómo una aplicación puede asegurarse de que se mantenga un árbol. Para exigir un árbol mediante restricciones, se puede crear una columna calculada que defina el elemento primario de cada nodo con una restricción de clave externa respecto al identificador de clave principal.  
  
```sql
CREATE TABLE Org_T3  
(  
   EmployeeId hierarchyid PRIMARY KEY,  
   ParentId AS EmployeeId.GetAncestor(1) PERSISTED    
      REFERENCES Org_T3(EmployeeId),  
   LastChild hierarchyid,   
   EmployeeName nvarchar(50)  
)  
GO  
```  
  
 Se prefiere este método que exige una relación cuando el código que no es de confianza para mantener el árbol jerárquico tiene acceso DML directo a la tabla. No obstante, este método puede reducir el rendimiento porque es necesario comprobar la restricción para cada operación DML.  
  
  
###  <a name="finding-ancestors-by-using-the-clr"></a><a name="findclr"></a> Buscar antecesores mediante CLR  
 Una operación común, en la que se implican dos nodos en una jerarquía, es buscar el antecesor común más bajo. Esto se puede escribir en [!INCLUDE[tsql](../includes/tsql-md.md)] o CLR porque el tipo de **hierarchyid** está disponible en ambos. Se recomienda CLR porque la ejecución es más rápida.  
  
 Use el siguiente código de CLR para hacer una lista de los antecesores y buscar el antecesor común más bajo:  
  
```csharp
using System;  
using System.Collections;  
using System.Text;  
using Microsoft.SqlServer.Server;  // SqlFunction Attribute
using Microsoft.SqlServer.Types;   // SqlHierarchyId
  
public partial class HierarchyId_Operations  
{  
    [SqlFunction(FillRowMethodName = "FillRow_ListAncestors")]
    public static IEnumerable ListAncestors(SqlHierarchyId h)
    {  
        while (!h.IsNull)  
        {  
            yield return (h);  
            h = h.GetAncestor(1);  
        }  
    }  
    public static void FillRow_ListAncestors(
        Object obj,
        out SqlHierarchyId ancestor
        )
    {  
        ancestor = (SqlHierarchyId)obj;  
    }  
  
    public static HierarchyId CommonAncestor(
        SqlHierarchyId h1,
        HierarchyId h2
        )  
    {  
        while (!h1.IsDescendantOf(h2))  
            h1 = h1.GetAncestor(1);  
  
        return h1;  
    }  
}  
```  
  
 Para usar los métodos **ListAncestor** y **CommonAncestor** en los siguientes ejemplos de [!INCLUDE[tsql](../includes/tsql-md.md)] , genere la DLL y cree el ensamblado de **HierarchyId_Operations** en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ejecutando un código similar al siguiente:  
  
```sql
CREATE ASSEMBLY HierarchyId_Operations   
    FROM '<path to DLL>\ListAncestors.dll';
GO  
```  
  
  
###  <a name="listing-ancestors"></a><a name="ancestors"></a> Enumerar antecesores  
 La creación de una lista de antecesores de un nodo es una operación común que sirve, por ejemplo, para mostrar la posición en una organización. Esto se puede realizar, por ejemplo, mediante una función con valores de tabla que use la clase **HierarchyId_Operations** definida anteriormente:  
  
 Usar [!INCLUDE[tsql](../includes/tsql-md.md)]:  
  
```sql
CREATE FUNCTION ListAncestors (@node hierarchyid)  
RETURNS TABLE (node hierarchyid)  
AS  
EXTERNAL NAME HierarchyId_Operations.HierarchyId_Operations.ListAncestors  
GO  
```  
  
 Ejemplo de uso:  
  
```sql
DECLARE @h hierarchyid  
SELECT @h = OrgNode   
FROM HumanResources.EmployeeDemo    
WHERE LoginID = 'adventure-works\janice0' -- /1/1/5/2/  
  
SELECT LoginID, OrgNode.ToString() AS LogicalNode  
FROM HumanResources.EmployeeDemo AS ED  
JOIN ListAncestors(@h) AS A   
   ON ED.OrgNode = A.Node  
GO  
```  
  
  
###  <a name="finding-the-lowest-common-ancestor"></a><a name="lowestcommon"></a> Buscar el antecesor común más bajo  
 Use la clase **HierarchyId_Operations** definida anteriormente para crear la siguiente función de [!INCLUDE[tsql](../includes/tsql-md.md)] a fin de buscar el antecesor común más bajo que implica dos nodos en una jerarquía:  
  
```sql
CREATE FUNCTION CommonAncestor (@node1 hierarchyid, @node2 hierarchyid)  
RETURNS hierarchyid  
AS  
EXTERNAL NAME HierarchyId_Operations.HierarchyId_Operations.CommonAncestor  
GO  
```  
  
 Ejemplo de uso:  
  
```sql
DECLARE @h1 hierarchyid, @h2 hierarchyid;
  
SELECT @h1 = OrgNode   
FROM  HumanResources.EmployeeDemo   
WHERE LoginID = 'adventure-works\jossef0'; -- Node is /1/1/3/  
  
SELECT @h2 = OrgNode   
FROM HumanResources.EmployeeDemo    
WHERE LoginID = 'adventure-works\janice0'; -- Node is /1/1/5/2/  
  
SELECT OrgNode.ToString() AS LogicalNode, LoginID   
FROM HumanResources.EmployeeDemo    
WHERE OrgNode = dbo.CommonAncestor(@h1, @h2) ;  
```  
  
 El nodo resultante es /1/1/  
  
  
###  <a name="moving-subtrees"></a><a name="BKMK_MovingSubtrees"></a> Mover los subárboles  
 Otra operación común es mover subárboles. El procedimiento siguiente toma el subárbol de **\@oldMgr** y lo convierte (incluido **\@oldMgr**) en un subárbol de **\@newMgr**.  
  
```sql
CREATE PROCEDURE MoveOrg(@oldMgr nvarchar(256), @newMgr nvarchar(256) )  
AS  
BEGIN  
DECLARE @nold hierarchyid, @nnew hierarchyid  
SELECT @nold = OrgNode FROM HumanResources.EmployeeDemo WHERE LoginID = @oldMgr ;  
  
SET TRANSACTION ISOLATION LEVEL SERIALIZABLE  
BEGIN TRANSACTION  
SELECT @nnew = OrgNode FROM HumanResources.EmployeeDemo WHERE LoginID = @newMgr ;  
  
SELECT @nnew = @nnew.GetDescendant(max(OrgNode), NULL)   
FROM HumanResources.EmployeeDemo WHERE OrgNode.GetAncestor(1)=@nnew ;  
  
UPDATE HumanResources.EmployeeDemo    
SET OrgNode = OrgNode.GetReparentedValue(@nold, @nnew)  
WHERE OrgNode.IsDescendantOf(@nold) = 1 ;  
  
COMMIT TRANSACTION;
END ;  
GO  
```  
  
  
## <a name="see-also"></a>Vea también  
 [Referencia de los métodos del tipo de datos hierarchyid](../t-sql/data-types/hierarchyid-data-type-method-reference.md)   
 [Tutorial: Uso del tipo de datos hierarchyid](../relational-databases/tables/tutorial-using-the-hierarchyid-data-type.md)   
 [hierarchyid &#40;Transact-SQL&#41;](../t-sql/data-types/hierarchyid-data-type-method-reference.md)  
  
