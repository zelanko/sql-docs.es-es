---
title: Introducción a SSMA para DB2 (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 48ca32fc-1830-4d1f-add7-480ba5ad02e8
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 0eab4f23e342c95d83baa70dd03aba2f5d4bc8d1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67989637"
---
# <a name="getting-started-with-ssma-for-db2-db2tosql"></a>Introducción a SSMA para DB2 (DB2ToSQL)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant (SSMA) para DB2 permite rápidamente convertir esquemas de base de datos de DB2 a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esquemas, cargar los esquemas resultantes a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y migrar datos desde DB2 a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
En este tema presenta el proceso de instalación y, a continuación, le ayuda a familiarizarse con la interfaz de usuario SSMA.  
  
## <a name="installing-ssma"></a>Instalación de SSMA  
Para usar SSMA, primero debe instalar el programa de cliente SSMA en un equipo que puede tener acceso a la base de datos de origen de DB2 y la instancia de destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Los proveedores OLE DB DB2 en el equipo que ejecuta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Estos componentes admiten la migración de datos y la emulación de funciones del sistema DB2. Para obtener instrucciones de instalación, consulte [instalar SSMA para DB2 &#40;DB2ToSQL&#41;](../../ssma/db2/installing-ssma-for-db2-db2tosql.md).  
  
Para iniciar SSMA, haga clic en **iniciar**, apunte a **todos los programas**, apunte a  **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant para DB2**y, a continuación, haga clic en  **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant para DB2**.  
  
## <a name="ssma-for-db2-user-interface"></a>SSMA para la interfaz de usuario de DB2  
Después de instala SSMA, puede usar SSMA para migrar bases de datos DB2 a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Ayuda a familiarizarse con la interfaz de usuario SSMA antes de empezar. El siguiente diagrama muestra la interfaz de usuario de SSMA, incluidos los exploradores de los metadatos, metadatos, las barras de herramientas, panel de salida y panel de lista de errores:  
  
![Interfaz de usuario SSMA](../../ssma/db2/media/ssma_db2_ui.png "interfaz de usuario SSMA")  
  
Para iniciar una migración, primero debe crear un nuevo proyecto. A continuación, se conecta a una base de datos DB2. Después de una conexión correcta, los esquemas de DB2 aparecerá en el Explorador de metadatos de DB2. Puede, a continuación, los objetos de botón derecho en el Explorador de metadatos de DB2 para realizar tareas como crean informes que evaluación las conversiones a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. También puede realizar estas tareas mediante el uso de los menús y barras de herramientas.  
  
También se debe conectar a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Después de una conexión correcta, una jerarquía de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bases de datos aparecerá en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Explorador de metadatos. Después de convertir los esquemas de DB2 a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esquemas, seleccione esos esquemas convertidos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] el Explorador de metadatos y, a continuación, sincronizar los esquemas con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
Después de sincronizar esquemas convertidos con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], puede volver al explorador de metadatos de DB2 y migrar datos de esquemas de DB2 en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bases de datos.  
  
Para obtener más información sobre estas tareas y cómo realizarlas, vea [migrar bases de datos DB2 a SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md).  
  
Las siguientes secciones describen las características de la interfaz de usuario SSMA.  
  
### <a name="metadata-explorers"></a>Exploradores de metadatos  
SSMA contiene dos exploradores de los metadatos para examinar y realizar acciones en DB2 y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bases de datos.  
  
#### <a name="db2-metadata-explorer"></a>DB2 Explorador de metadatos  
Explorador de metadatos de DB2 se muestra información acerca de los esquemas de DB2. Mediante el Explorador de metadatos de DB2, puede realizar las siguientes tareas:  
  
-   Examinar los objetos de cada esquema.  
  
-   Seleccionar objetos para la conversión y, a continuación, convertir los objetos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sintaxis. Para obtener más información, consulte [convertir esquemas de DB2 &#40;DB2ToSQL&#41;](../../ssma/db2/converting-db2-schemas-db2tosql.md).  
  
-   Seleccionar tablas para la migración de datos y, a continuación, migrar los datos de esas tablas a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener más información, consulte [migrar bases de datos DB2 a SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md).  
  
#### <a name="sql-server-metadata-explorer"></a>Explorador de metadatos SQL Server  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Explorador de metadatos muestra información acerca de una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Cuando se conecta a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], SSMA recupera los metadatos sobre esa instancia y la almacena en el archivo de proyecto.  
  
Puede usar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Explorador de metadatos para seleccionar los objetos de base de datos de DB2 convertidos y, a continuación, sincroniza esos objetos con la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
### <a name="metadata"></a>Metadatos  
A la derecha de cada explorador de metadatos son las pestañas que describen el objeto seleccionado. Por ejemplo, si selecciona una tabla en el Explorador de metadatos de DB2, aparecerán seis pestañas: **Tabla**, **SQL**, **asignación, el informe de tipo**, **propiedades**, y **datos**. El **informe** pestaña contiene información únicamente después de crear un informe que contiene el objeto seleccionado. Si selecciona una tabla en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] el Explorador de metadatos, aparecerán tres fichas: **Tabla**, **SQL**, y **datos**.  
  
La mayoría de los metadatos configuración es de solo lectura. Sin embargo, puede modificar los metadatos siguientes:  
  
-   En el Explorador de metadatos de DB2, puede modificar los procedimientos y asignaciones de tipos. Para convertir los procedimientos modificados y asignaciones de tipos, realice los cambios antes de convertir los esquemas.  
  
-   En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] el Explorador de metadatos, puede modificar el [!INCLUDE[tsql](../../includes/tsql-md.md)] para los procedimientos almacenados. Para ver estos cambios en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], realice estos cambios antes de cargar los esquemas a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
Los cambios realizados en el Explorador de metadatos se reflejan en los metadatos del proyecto, no en las bases de datos de origen o destino.  
  
### <a name="toolbars"></a>Barras de herramientas  
SSMA tiene dos barras de herramientas: una barra de herramientas de proyecto y una barra de herramientas de migración.  
  
#### <a name="the-project-toolbar"></a>La barra de herramientas de proyecto  
La barra de herramientas de proyecto contiene botones para trabajar con proyectos, conectar a DB2 y conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Estos botones son similares a los comandos en el **archivo** menú.  
  
#### <a name="migration-toolbar"></a>Barra de herramientas de migración  
La siguiente tabla muestra los comandos de la barra de herramientas de la migración:  
  
|Botón|Función|  
|------|--------|  
|**Crear informe**|Convierte los objetos seleccionados de DB2 a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sintaxis y, a continuación, crea un informe que muestra cómo se realiza correctamente la conversión.<br /><br />Este comando está deshabilitado a menos que los objetos seleccionados en el Explorador de metadatos de DB2.|  
|**Convertir esquema**|Convierte los objetos seleccionados de DB2 a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] objetos.<br /><br />Este comando está deshabilitado a menos que los objetos seleccionados en el Explorador de metadatos de DB2.|  
|**Migración de datos**|Migra los datos de la base de datos DB2 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Antes de ejecutar este comando, debe convertir los esquemas de DB2 a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esquemas y, a continuación, cargar los objetos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br />Este comando está deshabilitado a menos que los objetos seleccionados en el Explorador de metadatos de DB2.|  
|**Detener**|Detiene el proceso actual.|  
  
### <a name="menus"></a>Menús  
La siguiente tabla muestra los menús SSMA.  
  
|Menú|Descripción|  
|----|-----------|  
|**Archivo**|Contiene comandos para trabajar con proyectos, conectar a DB2 y conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**Editar**|Contiene comandos para buscar y trabajar con texto en las páginas de detalles, como copiar [!INCLUDE[tsql](../../includes/tsql-md.md)] desde el panel de detalles SQL. También contiene el **administrar marcadores** opción, donde podrá ver una lista de los marcadores existentes. Puede usar los botones en el lado derecho del cuadro de diálogo para administrar los marcadores.|  
|**Vista**|Contiene el **sincronizar metadatos Explorers** comando. Que sincroniza los objetos entre el Explorador de metadatos de DB2 y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Explorador de metadatos. También contiene comandos para mostrar y ocultar el **salida** y **lista de errores** paneles y una opción **diseños** para administrar los diseños.|  
|**Herramientas**|Contiene comandos para crear informes y migrar objetos y datos. También proporciona acceso a la **configuración Global** y **configuración del proyecto** cuadros de diálogo.|  
|**Ayuda**|Proporciona acceso para ayudar a SSMA y a la **sobre** cuadro de diálogo.|  
  
### <a name="output-pane-and-error-list-pane"></a>Panel de salida y el panel de lista de errores  
El **vista** menú proporciona comandos para alternar la visibilidad de los paneles de salida y el panel de lista de errores:  
  
-   El panel de resultados muestra los mensajes de estado de SSMA durante la conversión de objetos, la sincronización del objeto y migración de datos.  
  
-   El panel de lista de errores, muestra un error, advertencia y mensajes informativos en una lista clasificable.  
  
## <a name="see-also"></a>Vea también  
[Migración de datos de DB2 en SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-data-into-sql-server-db2tosql.md)  
[Referencia de la interfaz de usuario &#40;DB2ToSQL&#41;](../../ssma/db2/user-interface-reference-db2tosql.md)  
  
