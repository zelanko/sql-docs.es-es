---
title: Exportar un inventario de acceso (AccessToSQL) | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-access
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
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
caps.latest.revision: 18
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 834b8d2b1be548a8be1114d6b536475eb52d4441
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/06/2018
---
# <a name="exporting-an-access-inventory-accesstosql"></a>Exportar un inventario de acceso (AccessToSQL)
Si tiene varias bases de datos de Access y no está seguro de cuáles para migrar a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], puede exportar un inventario de todas las bases de datos de Access en un proyecto. A continuación, puede revisar y consultar los metadatos de inventario para determinar qué bases de datos y objetos de las bases de datos para migrar. Este inventario le permite rápidamente en encontrar respuestas a preguntas como las siguientes:  
  
-   ¿Cuáles son las bases de datos más grandes?  
  
-   ¿Quién posee la mayoría de las bases de datos?  
  
-   ¿Bases de datos que contienen las mismas tablas?  
  
-   ¿Qué bases de datos no se han modificado en los últimos seis meses?  
  
-   ¿Bases de datos que contienen información privada?  
  
Se proporcionan ejemplos de consultas que se utilizan para responder a estas preguntas al final de este tema.  
  
## <a name="exported-metadata"></a>Metadatos exportados  
SSMA exporta metadatos sobre el acceso a las bases de datos, tablas, columnas, índices, claves externas, las consultas, informes, formularios, macros y módulos. Metadatos acerca de cada una de estas categorías de elementos se exportan a una tabla independiente. Para los esquemas de estas tablas, vea [acceso inventario esquemas](http://msdn.microsoft.com/en-us/fdd3cff2-4d62-4395-8acf-71ea8f17f524).  
  
## <a name="exporting-inventory-data"></a>Exportar datos de inventario  
Para exportar un inventario de acceso, debe abrir por primera vez o crear un proyecto de SSMA y, a continuación, agregue la base de datos de Access que se desea analizar. Después de agregar las bases de datos a un proyecto SSMA, exportar los metadatos acerca de las bases de datos a un determinado [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] base de datos y esquema. Si es necesario, SSMA crea tablas para almacenar los metadatos. SSMA, a continuación, agrega los metadatos sobre las bases de datos de acceso a la [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] base de datos.  
  
> [!NOTE]  
> Una base de datos de Access se puede dividir en varios archivos: una base de datos de back-end que contiene tablas y bases de datos front-end que contienen consultas, formularios, informes, macros, módulos y accesos directos. Si desea migrar una base de datos de división para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], agregar la base de datos front-end SSMA.  
  
Las instrucciones siguientes describen cómo crear un proyecto, agregar las bases de datos al proyecto, conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]y, a continuación, exportar los datos de inventario.  
  
**Para crear un proyecto**  
  
1.  Abra SSMA para Access.  
  
2.  En el menú **Archivo**, seleccione **Nuevo proyecto**.  
  
    Aparecerá el cuadro de diálogo **Nuevo proyecto** .  
  
3.  En el **nombre** cuadro, escriba un nombre para el proyecto.  
  
4.  En el **ubicación** cuadro, escriba o seleccione una carpeta para el proyecto.  
  
5.  En el **Migrate To** combinado, seleccione la versión de destino al que desea migrar y, a continuación, haga clic en **Aceptar**.  
  
Para obtener más información sobre cómo crear proyectos, vea [crear y administrar proyectos](http://msdn.microsoft.com/en-us/f2d1f0b0-5394-4adb-b3f3-abd71eb68ca7).  
  
**Para buscar y agregar las bases de datos**  
  
1.  En el **archivo** menú, haga clic en **buscar bases de datos**.  
  
2.  En el Asistente para buscar las bases de datos, especifique la unidad, ruta de acceso de archivo o la ruta de acceso UNC que se va a buscar. O bien, haga clic en **examinar** para seleccionar la unidad o carpeta de red.  
  
3.  Haga clic en **agregar** para agregar la ubicación en el cuadro de lista.  
  
    Repita los dos pasos anteriores para agregar ubicaciones de búsqueda adicionales.  
  
4.  Opcionalmente, agregue los criterios de búsqueda para perfeccionar la lista de bases de datos que se devuelven.  
  
    > [!IMPORTANT]  
    > El **todo o parte del nombre de archivo** cuadro de texto no admite caracteres comodín.  
  
5.  Haga clic en **examinar**.  
  
    Aparece la página de análisis. Esto muestra las bases de datos que se han encontrado y el progreso de la búsqueda. Para detener la búsqueda, haga clic en **detener**.  
  
6.  En la página Seleccionar archivos, seleccione cada base de datos que desea agregar al proyecto.  
  
    Puede usar el **seleccionar todo** y **Borrar todo** botones en la parte superior de la lista para seleccionar o borrar todas las bases de datos. También puede presionada la tecla CTRL para seleccionar varias filas, o mantenga presionada la tecla MAYÚS hacia abajo para seleccionar un intervalo de filas.  
  
7.  Haga clic en **Siguiente**.  
  
8.  En la página de comprobación, haga clic en **finalizar**.  
  
Para obtener más información acerca de cómo agregar bases de datos a los proyectos, vea [agregar y quitar archivos de base de datos de Access](http://msdn.microsoft.com/en-us/e944c740-4c8a-4bc1-b0ed-be57bc06dced).  
  
**Para conectarse a SQL Server**  
  
1.  En el **archivo** menú, seleccione **conectar con SQL Server**.  
  
2.  En el cuadro de diálogo de conexión, escriba o seleccione el nombre de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
    -   Si se conecta a la instancia predeterminada en el equipo local, puede escribir **localhost** o un punto (**.**).  
  
    -   Si se conecta a la instancia predeterminada en otro equipo, escriba el nombre del equipo.  
  
    -   Si se conecta a una instancia con nombre, escriba el nombre del equipo, una barra diagonal inversa y el nombre de instancia. Por ejemplo: MyServer\MyInstance.  
  
3.  En el **base de datos** cuadro, escriba el nombre de la base de datos de destino para los metadatos exportados.  
  
4.  Si la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] está configurado para aceptar conexiones en un puerto no predeterminado, escriba el número de puerto que se utiliza para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] conexiones en el **puerto del servidor** cuadro. Para la instancia predeterminada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], el número de puerto predeterminado es 1433. Para las instancias con nombre, SSMA intenta obtener el número de puerto desde el [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] servicio Browser.  
  
5.  En el **autenticación** menú de lista desplegable, seleccione el tipo de autenticación que se usará para la conexión. Para usar la cuenta de Windows actual, seleccione **autenticación de Windows**. Para usar un [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] inicio de sesión, seleccione **autenticación de SQL Server**y, a continuación, proporcione un nombre de usuario y una contraseña.  
  
Para obtener más información sobre cómo conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], consulte [conectarse a SQL Server &#40;AccessToSQL&#41;](../../ssma/access/connecting-to-sql-server-accesstosql.md).  
  
**Para exportar información de inventario**  
  
1.  En el Explorador de metadatos de acceso, expanda **acceso metabase**.  
  
2.  Active la casilla situada junto a **bases de datos**.  
  
    Para omitir las bases de datos individuales u objetos de base de datos, expanda la **bases de datos** carpeta y, a continuación, desactive la casilla de verificación situada junto a la base de datos u objeto de base de datos.  
  
3.  Haga clic en **bases de datos** y seleccione **Exportar esquema**.  
  
4.  En el **Seleccionar esquema para la exportación de** cuadro de diálogo, seleccione el esquema de destino para los metadatos exportados y, a continuación, haga clic en **Aceptar**.  
  
Cada vez que exporta los metadatos, SSMA anexa los datos para el inventario. Los datos existentes en el inventario no se actualiza o elimina.  
  
## <a name="querying-the-exported-metadata"></a>Consultar los metadatos exportados  
Después de exportar los metadatos acerca de las bases de datos de Access, puede consultar los metadatos. Las instrucciones siguientes describen para utilizar la ventana del Editor de consultas en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] para ejecutar consultas.  
  
**Para consultar metadatos**  
  
1.  Desde el **iniciar** menú, elija **todos los programas**, seleccione **Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005** o a **Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008** o a **Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012**y, a continuación, haga clic en **SQL Server Management Studio**.  
  
2.  En el **conectar al servidor** cuadro de diálogo, compruebe la configuración y, a continuación, haga clic en **conectar**.  
  
3.  En la barra de herramientas de Management Studio, haga clic en **nueva consulta** para abrir el Editor de consultas.  
  
4.  En la ventana del Editor de consultas, escriba una consulta. En la sección siguiente se muestran algunos ejemplos.  
  
5.  Presione la tecla F5 para ejecutar la consulta.  
  
## <a name="query-examples"></a>Ejemplos de consultas  
Antes de ejecutar cualquiera de las siguientes consultas, debe ejecutar un uso *database_name* consulta para asegurarse de que las consultas se ejecutan en la base de datos que contiene los metadatos exportados. Por ejemplo, si exporta metadatos a una base de datos denominada MyAccessMetadata, podría agregar lo siguiente al principio de la [!INCLUDE[tsql](../../includes/tsql_md.md)] código:  
  
```  
USE MyAccessMetadata;  
GO  
```  
Todos los ejemplos siguientes se usa el **dbo** esquema. Si exporta los metadatos a otro esquema, asegúrese de cambiar el esquema al ejecutar estas consultas.  
  
### <a name="what-tables-and-columns-are-in-these-databases"></a>¿Qué tablas y columnas son en estas bases de datos?  
La consulta siguiente combina las tablas que contienen los metadatos de la base de datos, tabla y columna y, a continuación, devuelve los nombres de todas las bases de datos, tablas y columnas, ordenadas por nombre de columna:  
  
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
La consulta siguiente devuelve el nombre de base de datos, el tamaño del archivo y el número de tablas en cada base de datos de Access, ordenado por tamaño de archivo:  
  
```  
SELECT DatabaseName, FileSize, TablesCount  
FROM dbo.SSMA_Access_InventoryDatabases  
ORDER BY FileSize DESC;  
```  
  
### <a name="who-is-the-owner-of-most-of-the-databases"></a>¿Quién es el propietario de la mayoría de las bases de datos?  
La consulta siguiente devuelve el nombre de la base de datos y el propietario de cada base de datos de Access, ordenado por propietario.  
  
```  
SELECT DatabaseName, FileOwner  
FROM dbo.SSMA_Access_InventoryDatabases  
ORDER BY FileOwner;  
```  
  
### <a name="which-databases-contain-the-same-tables"></a>¿Bases de datos que contienen las mismas tablas?  
La siguiente consulta utiliza una subconsulta para buscar todos los nombres de tabla que aparecen más de una vez en la lista de tablas y, a continuación, utiliza esta lista de tablas para obtener el nombre de la base de datos. Los resultados se devuelven como el nombre de la base de datos y, a continuación, el nombre de tabla y se ordenan por nombre de la tabla.  
  
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
La consulta siguiente obtiene la fecha actual, obtiene el valor de mes de seis meses y, a continuación, devuelve una lista de bases de datos con una fecha de modificación de más de seis meses.  
  
```  
SELECT DatabaseName, DateModified  
FROM dbo.SSMA_Access_InventoryDatabases  
WHERE DATEDIFF(month, DateModified, GETDATE()) > 6  
ORDER BY DateModified;  
```  
  
### <a name="which-databases-contain-private-information"></a>¿Bases de datos que contienen información privada?  
Las bases de datos de acceso podrían contener información confidencial o personal. Es posible que desee mover estas bases de datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] para aprovechar sus características de seguridad. Si sabe que tienen un nombre específico las columnas que contienen datos confidenciales o contienen caracteres específicos, puede utilizar una consulta para buscar todas las columnas que contienen dicha información. Por ejemplo, puede buscar todas las columnas que contienen la cadena "Salario".  La consulta, a continuación, devuelve el nombre de la base de datos, el nombre de la tabla y el nombre de columna.  
  
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
[Preparar las bases de datos de acceso para la migración](http://msdn.microsoft.com/en-us/9b80a9e0-08e7-4b4d-b5ec-cc998d3f5114)  
  
