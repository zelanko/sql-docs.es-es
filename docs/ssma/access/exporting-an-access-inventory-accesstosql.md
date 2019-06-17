---
title: Exportación de un inventario de Access (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Access databases
- Access databases, exporting metadata
- exporting
- exporting Access metadata
- exporting, Access metadata
- exporting, querying exported metadata
- inventories of Access databases
- querying exported metadata
ms.assetid: 7e1941fb-3d14-4265-aff6-c77a4026d0ed
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: f35ae03cb6588bc7828349dd4a4beafcc5a7b2f3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62760832"
---
# <a name="exporting-an-access-inventory-accesstosql"></a>Exportación de un inventario de Access (AccessToSQL)
Si tiene varias bases de datos de Access y no está seguro de cuáles para migrar a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], puede exportar un inventario de todas las bases de datos de Access en un proyecto. A continuación, puede revisar y consultar los metadatos de inventario para determinar qué bases de datos y objetos dentro de esas bases de datos para migrar. Este inventario le permite rápidamente buscar respuestas a preguntas como las siguientes:  
  
-   ¿Cuáles son las bases de datos más grandes?  
  
-   ¿Quién posee la mayoría de las bases de datos?  
  
-   ¿Bases de datos que contienen las mismas tablas?  
  
-   ¿Qué bases de datos no se han modificado en los últimos seis meses?  
  
-   ¿Bases de datos que contienen información privada?  
  
Se proporcionan ejemplos de consultas que se usan para responder a estas preguntas al final de este tema.  
  
## <a name="exported-metadata"></a>Metadatos exportados  
SSMA exporta metadatos sobre el acceso a bases de datos, tablas, columnas, índices, claves externas, las consultas, informes, formularios, macros y módulos. Los metadatos sobre cada una de estas categorías de elementos se exportan a una tabla independiente. Los esquemas de estas tablas, consulte [esquemas de inventario de Access](access-inventory-schemas-accesstosql.md).  
  
## <a name="exporting-inventory-data"></a>Exportar datos de inventario  
Para exportar un inventario de Access, debe abrir por primera vez o crear un proyecto de SSMA y, a continuación, agregue la base de datos que desea analizar. Después de agregar las bases de datos a un proyecto SSMA, exportar los metadatos sobre esas bases de datos para un determinado [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] base de datos y esquema. Si es necesario, SSMA crea tablas para almacenar los metadatos. SSMA, a continuación, agrega los metadatos acerca de las bases de datos de acceso a la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] base de datos.  
  
> [!NOTE]  
> Una base de datos de Access se puede dividir en varios archivos: una base de datos de back-end que contiene las tablas y bases de datos front-end que contienen consultas, formularios, informes, macros, módulos y los accesos directos. Si desea migrar una base de datos división [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], agregue la base de datos front-end para SSMA.  
  
Las instrucciones siguientes describen cómo crear un proyecto, agregue las bases de datos al proyecto, conéctese a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]y, a continuación, exportar los datos de inventario.  
  
**Para crear un proyecto**  
  
1.  Abra SSMA para Access.  
  
2.  En el menú **Archivo**, seleccione **Nuevo proyecto**.  
  
    Aparecerá el cuadro de diálogo **Nuevo proyecto** .  
  
3.  En el **nombre** , escriba un nombre para el proyecto.  
  
4.  En el **ubicación** cuadro, escriba o seleccione una carpeta para el proyecto.  
  
5.  En el **Migrate To** combinado, seleccione la versión de destino al que desea migrar y, a continuación, haga clic en **Aceptar**.  
  
Para obtener más información sobre cómo crear proyectos, vea [crear y administrar proyectos](creating-and-managing-projects-accesstosql.md).  
  
**Para buscar y agregar las bases de datos**  
  
1.  En el **archivo** menú, haga clic en **buscar bases de datos**.  
  
2.  En el Asistente para buscar las bases de datos, especifique la unidad, ruta de acceso de archivo o la ruta de acceso UNC que desea buscar. Como alternativa, haga clic en **examinar** para seleccionar la unidad o carpeta de red.  
  
3.  Haga clic en **agregar** para agregar la ubicación en el cuadro de lista.  
  
    Repita los dos pasos anteriores para agregar ubicaciones de búsqueda adicionales.  
  
4.  Opcionalmente, agregue los criterios de búsqueda para restringir la lista de bases de datos que se devuelven.  
  
    > [!IMPORTANT]  
    > El **todo o parte del nombre de archivo** cuadro de texto no admite caracteres comodín.  
  
5.  Haga clic en **Scan**.  
  
    Aparece la página de análisis. Esto muestra las bases de datos que se han encontrado y el progreso de la búsqueda. Para detener la búsqueda, haga clic en **detener**.  
  
6.  En la página Seleccionar archivos, seleccione cada base de datos que desea agregar al proyecto.  
  
    Puede usar el **seleccionar todo** y **Borrar todo** botones en la parte superior de la lista para seleccionar o borrar todas las bases de datos. También puede presionada la tecla CTRL para seleccionar varias filas, o mantenga presionada la tecla MAYÚS hacia abajo para seleccionar un intervalo de filas.  
  
7.  Haga clic en **Siguiente**.  
  
8.  En la página de comprobación, haga clic en **finalizar**.  
  
Para obtener más información acerca de cómo agregar bases de datos a los proyectos, vea [agregar y quitar archivos de base de datos de Access](adding-and-removing-access-database-files-accesstosql.md).  
  
**Para conectarse a SQL Server**  
  
1.  En el **archivo** menú, seleccione **conectar con SQL Server**.  
  
2.  En el cuadro de diálogo de conexión, escriba o seleccione el nombre de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
    -   Si se conecta a la instancia predeterminada en el equipo local, puede escribir **localhost** o un punto ( **.** ).  
  
    -   Si se conecta a la instancia predeterminada en otro equipo, escriba el nombre del equipo.  
  
    -   Si se conecta a una instancia con nombre, escriba el nombre del equipo, una barra diagonal inversa y el nombre de instancia. Por ejemplo: MyServer\MyInstance.  
  
3.  En el **base de datos** , escriba el nombre de la base de datos de destino para los metadatos exportados.  
  
4.  Si la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está configurado para aceptar conexiones en un puerto no predeterminado, escriba el número de puerto que se utiliza para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conexiones en el **puerto del servidor** cuadro. Para la instancia predeterminada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el número de puerto predeterminado es 1433. Las instancias con nombre, SSMA intenta obtener el número de puerto desde el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] servicio Browser.  
  
5.  En el **autenticación** menú de lista desplegable, seleccione el tipo de autenticación que se usará para la conexión. Para usar la cuenta de Windows actual, seleccione **Windows autenticación**. Para usar un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inicio de sesión, seleccione **autenticación de SQL Server**y, a continuación, proporcione un nombre de usuario y una contraseña.  
  
Para obtener más información sobre cómo conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [conectarse a SQL Server &#40;AccessToSQL&#41;](../../ssma/access/connecting-to-sql-server-accesstosql.md).  
  
**Para exportar información de inventario**  
  
1.  En el Explorador de metadatos de acceso, expanda **acceso de metabase**.  
  
2.  Active la casilla situada junto a **bases de datos**.  
  
    Para omitir las bases de datos individuales o los objetos de base de datos, expanda el **bases de datos** carpeta y, a continuación, desactive la casilla de verificación situada junto a la base de datos o el objeto de base de datos.  
  
3.  Haga clic en **bases de datos** y seleccione **Exportar esquema**.  
  
4.  En el **Seleccionar esquema para la exportación** cuadro de diálogo, seleccione el esquema de destino para los metadatos exportados y, a continuación, haga clic en **Aceptar**.  
  
Cada vez que exporta los metadatos, SSMA anexa los datos para el inventario. Los datos existentes en el inventario no se actualiza o elimina.  
  
## <a name="querying-the-exported-metadata"></a>Consultar los metadatos exportados  
Después de exportar los metadatos sobre las bases de datos de Access, puede consultar los metadatos. Las instrucciones siguientes describen para usar la ventana del Editor de consultas en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para ejecutar consultas.  
  
**Para consultar los metadatos**  
  
1.  Desde el **iniciar** menú, elija **todos los programas**, apunte a **Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005** o a **Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008**o a **Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012**y, a continuación, haga clic en **SQL Server Management Studio**.  
  
2.  En el **conectar al servidor** cuadro de diálogo, compruebe la configuración y, a continuación, haga clic en **Connect**.  
  
3.  En la barra de herramientas de Management Studio, haga clic en **nueva consulta** para abrir el Editor de consultas.  
  
4.  En la ventana del Editor de consultas, escriba una consulta. En la sección siguiente se muestran algunos ejemplos.  
  
5.  Presione la tecla F5 para ejecutar la consulta.  
  
## <a name="query-examples"></a>Ejemplos de consultas  
Antes de ejecutar cualquiera de las consultas siguientes, debe ejecutar un uso *database_name* consulta para asegurarse de que las consultas se ejecutan en la base de datos que contiene los metadatos exportados. Por ejemplo, si exporta los metadatos para una base de datos denominada MyAccessMetadata, debe agregar la siguiente al principio de la [!INCLUDE[tsql](../../includes/tsql-md.md)] código:  
  
```  
USE MyAccessMetadata;  
GO  
```  
Todos los ejemplos siguientes se usa el **dbo** esquema. Si exporta los metadatos a otro esquema, no olvide cambiar el esquema al ejecutar estas consultas.  
  
### <a name="what-tables-and-columns-are-in-these-databases"></a>¿Qué tablas y columnas están en estas bases de datos?  
La siguiente consulta combina las tablas que contienen los metadatos de la base de datos, tabla y columna y, a continuación, devuelve los nombres de todas las bases de datos, tablas y columnas, ordenadas por nombre de columna:  
  
```  
SELECT DatabaseName, TableName, ColumnName   
FROM dbo.SSMA_Access_InventoryColumns C  
JOIN dbo.SSMA_Access_InventoryTables T  
ON C.TableId = T.TableId  
JOIN dbo.SSMA_Access_InventoryDatabases D  
ON T.DatabaseId = D.DatabaseId  
ORDER BY ColumnName;  
```  
  
### <a name="what-are-the-largest-databases"></a>¿Cuáles son las bases de datos más grandes?  
La consulta siguiente devuelve el nombre de la base de datos, el tamaño de archivo y el número de tablas en cada base de datos de Access, ordenado por tamaño de archivo:  
  
```  
SELECT DatabaseName, FileSize, TablesCount  
FROM dbo.SSMA_Access_InventoryDatabases  
ORDER BY FileSize DESC;  
```  
  
### <a name="who-is-the-owner-of-most-of-the-databases"></a>¿Quién es el propietario de la mayoría de las bases de datos?  
La consulta siguiente devuelve el nombre de la base de datos y el propietario de cada base de datos de Access, ordenado por el propietario.  
  
```  
SELECT DatabaseName, FileOwner  
FROM dbo.SSMA_Access_InventoryDatabases  
ORDER BY FileOwner;  
```  
  
### <a name="which-databases-contain-the-same-tables"></a>¿Bases de datos que contienen las mismas tablas?  
La consulta siguiente utiliza una subconsulta para buscar todos los nombres de tabla que aparecen más de una vez en la lista de tablas y, a continuación, usa esta lista de tablas para obtener el nombre de la base de datos. Los resultados se devuelven como el nombre de la base de datos y, a continuación, el nombre de tabla y se ordenan por nombre de tabla.  
  
```  
SELECT DatabaseName, TableName   
FROM dbo.SSMA_Access_InventoryTables T  
JOIN dbo.SSMA_Access_InventoryDatabases D  
ON D.DatabaseId = T.DatabaseId  
WHERE TableName IN (  
SELECT TableName   
FROM dbo.SSMA_Access_InventoryTables  
GROUP BY TableName   
HAVING count(*)>1  
)  
ORDER BY TableName;  
```  
  
### <a name="which-databases-were-not-modified-in-the-last-six-months"></a>¿Qué bases de datos no se han modificado en los últimos seis meses?  
La consulta siguiente obtiene la fecha actual, obtiene el valor de mes de hace seis meses y, a continuación, devuelve una lista de bases de datos con una fecha de modificación de más de hace seis meses.  
  
```  
SELECT DatabaseName, DateModified  
FROM dbo.SSMA_Access_InventoryDatabases  
WHERE DATEDIFF(month, DateModified, GETDATE()) > 6  
ORDER BY DateModified;  
```  
  
### <a name="which-databases-contain-private-information"></a>¿Bases de datos que contienen información privada?  
Las bases de datos de acceso podrían contener información confidencial o personal. Es posible que desee mover estas bases de datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para aprovechar sus características de seguridad. Si sabe que tienen un nombre específico las columnas que contienen datos confidenciales o contienen caracteres específicos, puede usar una consulta para buscar todas las columnas que contienen esa información. Por ejemplo, puede encontrar todas las columnas que contienen la cadena "Salario".  La consulta, a continuación, devuelve el nombre de la base de datos, el nombre de la tabla y el nombre de columna.  
  
```  
SELECT DatabaseName, TableName, ColumnName   
FROM dbo.SSMA_Access_InventoryColumns C  
JOIN dbo.SSMA_Access_InventoryTables T  
ON C.TableId = T.TableId  
JOIN dbo.SSMA_Access_InventoryDatabases D  
ON T.DatabaseId = D. DatabaseId  
WHERE ColumnName LIKE '%salary%';  
```  
Si no conoce el nombre de columna, puede escribir una consulta para devolver todas las columnas. Para ello, quite la cláusula WHERE de la consulta anterior.  
  
## <a name="see-also"></a>Vea también  
[Preparar las bases de datos de acceso para la migración](preparing-access-databases-for-migration-accesstosql.md)  
  
