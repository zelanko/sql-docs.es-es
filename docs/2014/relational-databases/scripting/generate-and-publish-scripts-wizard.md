---
title: Asistente generar y publicar scripts
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- sql12.swb.generatescriptswizard.setscriptingoptions.f1
- sql9.swb.generatescriptswizard.scriptwizarddescription.f1
- sql12.swb.generatescriptswizard.saveorpublishscripts.f1
- sql9.swb.generatescriptswizard.selectdatabase.f1
- sql9.swb.generatescriptswizard.scriptfileoption.f1
- sql12.swb.generatescriptswizard.advancedscriptingoptions.f1
- sql9.swb.generatescriptswizard.choosescriptoptions.f1
- sql12.swb.generatescriptswizard.summarypage.f1
- sql9.swb.generatescriptswizard.chooseviews.f1
- sql12.swb.generatescriptswizard.providerconfiguration.f1
- sql9.swb.generatescriptswizard.choosestoredprocedures.f1
- sql9.swb.generatescriptswizard.chooseobjecttypes.f1
- sql9.swb.generatescriptswizard.welcome.f1
- sql9.swb.generatescriptswizard.chooseudf.f1
- sql12.swb.generatescriptswizard.manageproviders.f1
- sql9.swb.generatescriptswizard.chooseuddt.f1
- sql12.swb.generatescriptswizard.advancedpublishingoptions.f1
- sql12.swb.generatescriptswizard.introduction.f1
- sql9.swb.generatescriptswizard.chooserules.f1
- sql12.swb.generatescriptswizard.chooseobjects.f1
- sql9.swb.generatescriptswizard.progress.f1
- sql9.swb.generatescriptswizard.choosedefaults.f1
- sql9.swb.generatescriptswizard.chooseobjects.f1
- sql9.swb.generatescriptswizard.choosetables.f1
helpviewer_keywords:
- databases [SQL Server], publishing
- publishing databases
- scripts [SQL Server], generating
- scripts [SQL Server], publishing
- databases [SQL Server], generating scripts
- Publish Database Wizard
ms.assetid: 5ee520ba-ec7e-4199-a441-189e9e264b37
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 47bf324dd757661a6f49f18b28f810c87ca1419e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "75242107"
---
# <a name="generate-and-publish-scripts-wizard"></a>Asistente generar y publicar scripts
  Puede usar el **Asistente Generar y publicar scripts** para crear scripts con el fin de transferir una base de datos entre instancias de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] o [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]. Puede generar scripts para una base de datos en una instancia del motor de base de datos en la red local o a partir de [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. Los scripts generados se pueden ejecutar en otra instancia del motor de base de datos o [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. También puede usar el asistente para publicar el contenido de una base de datos directamente en un servicio web creado usando Database Publishing Services. Es posible crear scripts para una base de datos completa o limitarlos a objetos específicos.  
  
1.  **Antes de empezar:**  [publicar en un servicio hospedado](#PubHostSvc), [permisos](#Permissions)  
  
2.  **Para generar o publicar un script con:**  [el asistente generar y publicar scripts](#GenPubScriptWiz)  
  
## <a name="before-you-begin"></a>Antes de empezar  
 Las bases de datos de origen y de destino pueden estar en [!INCLUDE[ssSDS](../../includes/sssds-md.md)]o en una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)] que ejecuta [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o una versión posterior.  
  
###  <a name="PubHostSvc"></a>Publicación en un servicio hospedado  
 Además de crear scripts, el **Asistente Generar y publicar scripts** se puede usar para publicar una base de datos en un tipo específico de servicio web hospedado de SQL Server. El SQL Server Hosting Toolkit proporciona Database Publishing Services como un proyecto de origen compartido en CodePlex. Los proveedores del hospedaje web pueden usar el proyecto Database Publishing Services para generar un conjunto de servicios web que faciliten a sus clientes la implementación de bases de datos en el servicio web. Para obtener más información sobre cómo descargar el SQL Server Hosting Toolkit, vea [SQL Server Database Publishing Services](https://go.microsoft.com/fwlink/?LinkId=142025).  
  
 Para publicar una base de datos a un servicio de hospedaje web, seleccione la opción **Publicar en servicio web** en la página **Establecer opciones de scripting** del asistente.  
  
###  <a name="Permissions"></a> Permisos  
 El permiso mínimo para publicar una base de datos es la pertenencia al rol fijo de base de datos db_ddladmin en la base de datos de origen. El permiso mínimo para publicar un script de base de datos en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el proveedor de hospedaje es la pertenencia al rol fijo de base de datos db_ddladmin en la base de datos de destino.  
  
 Para publicar con el asistente, el usuario también debe proporcionar un nombre de usuario y una contraseña para tener acceso a su cuenta en el proveedor de hospedaje. La base de datos destino se debe crear en el proveedor del hospedaje antes de que la base de datos de origen se publique. Al publicar, se sobrescriben los objetos presentes en la base de datos.  
  
##  <a name="GenPubScriptWiz"></a>Usar el asistente generar y publicar scripts  
 **Para generar un script de publicación**  
  
1.  En **Explorador de objetos**, expanda el nodo de la instancia que contiene la base de datos que se va a incluir en el script.  
  
2.  Seleccione **Tareas**y, a continuación, haga clic en **Generar scripts**.  
  
3.  Complete los cuadros de diálogo del asistente:  
  
    -   [Página Introducción](#Introduction)  
  
    -   [Página Elegir objetos](#ChooseObjects)  
  
    -   [Página Establecer opciones de scripting](#SetScriptOpt)  
  
    -   [Página Opciones de scripting avanzadas](#AdvScriptOpt)  
  
    -   [Página Proveedores administrados](#MgProviders)  
  
    -   [Página Opciones de publicación avanzadas](#AdvPubOpts)  
  
    -   [Página Configuración de proveedor](#ProvConfig)  
  
    -   [Página Resumen](#Summary)  
  
    -   [Página Guardar o publicar scripts](#SavePubScripts)  
  
###  <a name="Introduction"></a> Página Introducción  
 Esta página describe los pasos para generar o publicar un script.  
  
 **No volver a mostrar esta página** : omite esta página la próxima vez que inicie el **asistente Generar y publicar scripts**.  
  
 **Siguiente >** : avanza a la página **elegir método** .  
  
 **Cancelar** : termina el asistente sin generar o publicar un script de la base de datos.  
  
###  <a name="ChooseObjects"></a>Página elegir objetos  
 Use esta página para elegir los objetos que desea incluir en los scripts generados por el asistente. En la siguiente página del asistente, podrá guardar estos scripts en la ubicación que elija o usarlos para publicar objetos de base de datos en un proveedor de hospedaje web remoto que tenga instalado [SQL Server Database Publishing Services](https://go.microsoft.com/fwlink/?LinkId=142025).  
  
 Incluir en el **script la opción de base de datos completa** : haga clic para generar scripts para todos los objetos de la base de datos e incluir un script para la propia base de datos.  
  
 **Seleccionar objetos de base de datos específicos** : haga clic en esta opción para limitar el asistente con el fin de que genere scripts solo para los objetos concretos de la base de datos que elija:  
  
-   **Objetos de base de datos** : seleccione al menos un objeto para incluirlo en el script.  
  
-   **Seleccionar todo** : activa todas las casillas disponibles.  
  
-   **Anular la selección** : desactiva todas las casillas. Para poder continuar, deberá seleccionar al menos un objeto de base de datos.  
  
###  <a name="SetScriptOpt"></a>Página establecer opciones de scripting  
 Use esta página para especificar si desea que el asistente guarde los scripts en la ubicación que elija o usarlos para publicar objetos de base de datos en un proveedor de hospedaje web remoto. Para publicar, debe tener acceso a un servicio web que se haya instalado mediante el servicio web Database Publishing Services Web.  
  
 **Opciones** : Si desea que el asistente guarde los scripts en la ubicación que elija, seleccione **Guardar scripts en una ubicación específica**. Posteriormente, podrá ejecutar los scripts con respecto a una instancia del motor de base de datos o [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. Si desea que el asistente publique los objetos de base de datos en un proveedor de hospedaje web remoto, seleccione **Publicar en servicio web**.  
  
 **Guardar scripts en una ubicación específica** : guarda uno o varios. Archivos de script de Transact-SQL en una ubicación que especifique.  
  
-   **Avanzadas** : muestra el cuadro de diálogo Opciones avanzadas de **scripting** en el que puede seleccionar las opciones avanzadas para generar scripts.  
  
-   **Guardar en el archivo** : Guarde el script en uno o varios archivos. SQL. Haga clic en el botón Examinar (**…**) para especificar el nombre y la ubicación del archivo. Active la casilla **Sobrescribir el archivo existente** para reemplazar el archivo si ya existe uno con el mismo nombre. Haga clic en **Un solo archivo** o en **Archivo único por objeto** para especificar el modo en que se deben generar los scripts. Haga clic en **Texto Unicode** o en **Texto ANSI** para especificar el tipo de texto que se debe usar en el script.  
  
-   **Guardar en el portapapeles** : guarda el script TRANSACT-SQL en el portapapeles.  
  
-   **Guardar en nueva ventana de consulta** : genera el script en una motor de base de datos ventana del editor de consultas. Si no hay ninguna ventana de editor abierta, se abre una nueva ventana como destino del script.  
  
 **Publicar en servicio Web** : publique los objetos que seleccionó en un servicio de hospedaje Web remoto para el que ha configurado un proveedor.  
  
-   **Administrar proveedores** : muestra el cuadro de diálogo **administrar proveedores** . Use el cuadro de diálogo **Proveedores administrados** para agregar, modificar y eliminar proveedores de hospedaje. Cada proveedor especifica la información de conexión a un servicio de hospedaje de sitios web y las bases de datos de destino en ese servicio.  
  
-   **Avanzadas** : muestra el cuadro de diálogo **Opciones de publicación avanzadas** , donde puede seleccionar opciones avanzadas para publicar scripts.  
  
-   **Proveedor** : seleccione el proveedor que especifica la información de conexión para el servicio de hospedaje web que hospeda la base de datos en la que desea publicar los objetos que ha seleccionado. Debe haber al menos un proveedor en el cuadro de diálogo **Proveedores administrados** para seleccionar un proveedor.  
  
-   **Base de datos de destino** : seleccione la base de datos de destino donde desea publicar los objetos que ha seleccionado. Debe seleccionar un proveedor antes de seleccionar una base de datos de destino.  
  
###  <a name="AdvScriptOpt"></a>Página opciones de scripting avanzadas  
 Use esta página para especificar cómo desea que este asistente genere los scripts. Hay disponibles numerosas opciones. Las opciones se atenúan si no se admiten en la versión de SQL Server o [!INCLUDE[ssSDS](../../includes/sssds-md.md)] especificada en **Tipo de motor de base de datos**.  
  
 **Opciones** : especifique las opciones avanzadas seleccionando un valor en la lista de configuraciones disponibles a la derecha de cada opción.  
  
 **General** : las opciones siguientes se aplican a todo el script.  
  
-   **Relleno ANSI** : incluye `ANSI PADDING ON` en el script. El valor predeterminado es **true**.  
  
-   **Anexar a archivo** : si es **true**, este script se agrega al final de un script existente, especificado en la página **establecer opciones de scripting** . Si es **False**, el nuevo script sobrescribe un script anterior. El valor predeterminado es **False**.  
  
-   **Continuar scripting en** caso de error: Si **es true**, el script se detiene cuando se produce un error. Si es **False**, el scripting continúa. El valor predeterminado es **False**.  
  
-   **Convertir UDDTs en tipos base** : Si **es true**, los tipos de datos definidos por el usuario (UDDT) se convierten en los tipos de datos base subyacentes que se usaron para crearlos. Use **True** cuando el UDDT no exista en la base de datos en la que se ejecutará el script. Si es **False**, se usan los UDDT. El valor predeterminado es **False**.  
  
-   **Generar script para objetos dependientes** : genera un script para cualquier objeto que deba estar presente cuando se ejecute el script para el objeto seleccionado. El valor predeterminado es **true**.  
  
-   **Incluir encabezados descriptivos** : Si **es true**, se agregan comentarios descriptivos al script que separa el script en secciones para cada objeto. El valor predeterminado es **False**.  
  
-   **Incluir if not EXISTS** : Si **es true**, el script incluye una instrucción para comprobar si el objeto ya existe en la base de datos y no intenta crear un nuevo objeto si el objeto ya existe. El valor predeterminado es **False**.  
  
-   **Incluir nombres de restricción del sistema** : Si **es false**, el valor predeterminado de las restricciones que se denominaron automáticamente en la base de datos de origen se vuelven a denominar automáticamente en la base de datos de destino. Si es **True**, las restricciones tienen el mismo nombre en las bases de datos de origen y de destino.  
  
-   **Incluir instrucciones no admitidas** : cuando **es false**, el script no contiene instrucciones para los objetos que no se admiten en la versión de servidor o tipo de motor seleccionados. Si es **True**, el script contiene los objetos no compatibles. Cada instrucción para un objeto no compatible tendrá un comentario que indica que se debe editar la instrucción antes de que el script pueda ejecutarse con respecto a la versión del SQL Server o tipo de motor seleccionados. El valor predeterminado es **False**.  
  
-   **Nombres de objeto de certificado de esquema** : incluye el nombre de esquema en el nombre de los objetos que se crean. El valor predeterminado es **true**.  
  
-   **Incluir enlaces** : genera un script para enlazar los objetos predeterminados y de regla. El valor predeterminado es **False**. Para obtener más información, vea [CREATE DEFAULT &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-default-transact-sql) y [CREATE RULE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-rule-transact-sql).  
  
-   **Incluir intercalación** : incluye información de intercalación en el script. El valor predeterminado es **False**. Para más información, consulte [Compatibilidad con la intercalación y Unicode](../collations/collation-and-unicode-support.md).  
  
-   Valores **predeterminados de script** : incluye los objetos predeterminados usados para establecer los valores predeterminados en las columnas de la tabla. El valor predeterminado es **true**. Para obtener más información, vea [CREATE DEFAULT &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-default-transact-sql).  
  
-   Incluir **Drop y Create** en el script: al [!INCLUDE[tsql](../../../includes/tsql-md.md)] crear el **script**, se incluyen instrucciones para crear objetos. Cuando se coloca el [!INCLUDE[tsql](../../../includes/tsql-md.md)] **script Drop**, se incluyen instrucciones para quitar objetos. Si es **Incluir DROP y CREATE en el script**, se incluye la instrucción DROP de [!INCLUDE[tsql](../../../includes/tsql-md.md)] en el script, seguida de la instrucción CREATE, por cada objeto del script. El valor predeterminado es **Incluir CREATE en el script**.  
  
-   **Generar script de propiedades extendidas** : incluye propiedades extendidas en el script si el objeto tiene propiedades extendidas. El valor predeterminado es **true**.  
  
-   **Script para tipo de motor** : crea un script que se puede ejecutar en el tipo seleccionado de [!INCLUDE[ssSDS](../../includes/sssds-md.md)] o en una instancia de la SQL Server motor de base de datos. Los objetos no admitidos en el tipo especificado no se incluyen en el script. El valor predeterminado es el tipo del servidor de origen.  
  
-   **Script para la versión de servidor** : crea un script que se puede ejecutar en la versión [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]seleccionada de. Las características nuevas de una versión no se pueden incluir en scripts para versiones anteriores. El valor predeterminado es la versión del servidor de origen.  
  
-   **Scripts de inicio de sesión** : cuando el objeto que se va a incluir en el script es un usuario de base de datos, esta opción crea los inicios de sesión de los que depende el usuario. El valor predeterminado es **False**.  
  
-   **Incluir permisos de nivel de objeto** en el script: incluye scripts para establecer el permiso en los objetos de la base de datos. El valor predeterminado es **False**.  
  
-   **Incluir estadísticas** en el script: cuando se establece en **incluir estadísticas**, `CREATE STATISTICS` esta opción incluye la instrucción para volver a crear estadísticas en el objeto. La opción **Incluir estadísticas e histogramas en el script** también crea información de histogramas. El valor predeterminado es **No incluir estadísticas en el script**. Para obtener más información, vea [CREATE STATISTICS &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-statistics-transact-sql).  
  
-   **Script de uso de base** de `USE DATABASE` datos: agrega la instrucción al script. Para asegurarse de que se creen objetos de base de datos en la base de datos correcta, incluya la instrucción `USE DATABASE`. Cuando se espera que el script se use en una base de datos diferente, seleccione **false** para `USE DATABASE` omitir la instrucción. El valor predeterminado es **true**. Para obtener más información, vea [USE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/use-transact-sql).  
  
-   **Tipos de datos para el script** : selecciona lo que se debe incluir en el script: **solo datos**, **solo esquema**o ambos. El valor predeterminado **Solo esquema**.  
  
 **Opciones de tabla o vista** : las siguientes opciones solo se aplican a scripts para tablas o vistas.  
  
-   **Script de seguimiento de cambios** : scripts de seguimiento de cambios si está habilitado en la base de datos de origen o en las tablas de la base de datos de origen. El valor predeterminado es **False**. Para obtener más información, vea [Acerca del seguimiento de cambios &#40;SQL Server&#41;](../track-changes/about-change-tracking-sql-server.md).  
  
-   **Incluir restricciones check** en el script: `CHECK` agrega restricciones al script. El valor predeterminado es **true**. Las restricciones `CHECK` requieren datos que se escriban en una tabla para cumplir con una condición especificada. Para más información, consulte [Unique Constraints and Check Constraints](../tables/unique-constraints-and-check-constraints.md).  
  
-   **Incluir opciones de compresión de datos** : scripts opciones de compresión de datos si están configuradas en la base de datos de origen o en las tablas de la base de datos de origen. Para obtener más información, consulte [Data Compression](../data-compression/data-compression.md). El valor predeterminado es **False**.  
  
-   **Incluir claves externas** en el script: agrega claves externas al script. El valor predeterminado es **true**. Las claves externas indican y exigen relaciones entre tablas.  
  
-   **Generar script de índices de texto completo** : incluye en el script la creación de índices de texto completo. El valor predeterminado es **False**.  
  
-   **Generar script de índices** : incluye en el script la creación de índices. El valor predeterminado es **true**. Los índices ayudan a encontrar rápidamente los datos.  
  
-   **Generar script de claves principales** : incluye en el script la creación de claves principales en las tablas. El valor predeterminado es **true**. Las claves principales identifican de forma exclusiva cada fila de una tabla.  
  
-   **Generar script de desencadenadores** : incluye en el script la creación de desencadenadores DML en las tablas. El valor predeterminado es **False**. Un desencadenador DML es una acción programada para ejecutarse cuando se produce un evento DML (lenguaje de manipulación de datos) en el servidor de base de datos. Para más información, consulte [DML Triggers](../triggers/dml-triggers.md).  
  
-   **Generar script de claves únicas** : incluye en el script la creación de claves únicas en las tablas. Las claves únicas evitan que se especifiquen datos duplicados. El valor predeterminado es **true**. Para más información, consulte [Unique Constraints and Check Constraints](../tables/unique-constraints-and-check-constraints.md).  
  
###  <a name="MgProviders"></a>Página administrar proveedores  
 Use este cuadro de diálogo para ver, agregar, modificar, eliminar o probar las conexiones del proveedor de hospedaje. Un proveedor de hospedaje especifica la información de conexión para un servicio web que se haya creado con el proyecto Database Publishing Services en SQL Server Hosting Toolkit en CodePlex.  
  
 **Proveedores configurados** : enumera el nombre y la dirección del servicio **Web** de cada proveedor de hospedaje que se ha guardado.  
  
 **Nuevo** : abre el cuadro **de diálogo Configuración de proveedor para nuevo proveedor** para agregar un nuevo proveedor de hospedaje.  
  
 **Editar** : abre el cuadro de diálogo **configuración de proveedor** correspondiente para modificar un proveedor de hospedaje existente.  
  
 **Eliminar** : elimina el proveedor de hospedaje seleccionado.  
  
 **Test: prueba** la conexión a un servicio de hospedaje mediante la información del proveedor seleccionado.  
  
 **Aceptar** : guarda todos los cambios realizados en el cuadro de diálogo **proveedor de hospedaje** .  
  
 **Cancelar** : Deshace todos los cambios realizados en el cuadro de diálogo **proveedor de hospedaje** .  
  
###  <a name="AdvPubOpts"></a>Página opciones de publicación avanzadas  
 Use esta página para especificar cómo desea que este asistente publique una base de datos. Hay disponibles numerosas opciones. Las opciones se atenúan si no se admiten en la versión de SQL Server o [!INCLUDE[ssSDS](../../includes/sssds-md.md)] especificada en **Tipo de motor de base de datos**.  
  
 **Opciones** : especifique las opciones avanzadas seleccionando un valor en la lista de configuraciones disponibles a la derecha de cada opción.  
  
 **General** : las opciones siguientes se aplican a toda la publicación.  
  
1.  **Convertir UDDTs en tipos base** : Si **es true**, los tipos de datos definidos por el usuario (UDDT) se convierten en los tipos de datos base subyacentes que se usaron para crearlos. Use **True** cuando el UDDT no exista en la base de datos en la que se ejecutará el script. Si es **False**, se usan los UDDT. El valor predeterminado es **False**.  
  
2.  **Publicar intercalación** : incluye información de intercalación para las columnas de la tabla. El valor predeterminado es **False**. Para más información, consulte [Compatibilidad con la intercalación y Unicode](../collations/collation-and-unicode-support.md).  
  
3.  **Publicar valores predeterminados** : incluye los objetos predeterminados que se usan para establecer valores predeterminados en las columnas de la tabla. El valor predeterminado es **true**. Para obtener más información, vea [CREATE DEFAULT &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-default-transact-sql).  
  
4.  **Publicar objetos dependientes** : publica cualquier objeto que deba estar presente cuando se ejecute el script para el objeto seleccionado. El valor predeterminado es **True**.  
  
5.  **Publicar propiedades extendidas** : incluye propiedades extendidas en el script que se envía al proveedor para su publicación, si el objeto tiene propiedades extendidas. El valor predeterminado es **true**.  
  
6.  **Publicar para la versión del servidor** : crea un script que se envía al proveedor remoto para su publicación de una manera que se puede ejecutar en la versión [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]seleccionada de. Las características nuevas de una versión no se pueden incluir en scripts para versiones anteriores. El valor predeterminado es la versión del servidor de origen.  
  
7.  **Publicar permisos de nivel de objeto** : incluye los permisos en los objetos seleccionados en la base de datos. El valor predeterminado es **False**.  
  
8.  **Publicar estadísticas** : cuando se establece para **publicar estadísticas**, incluye `CREATE STATISTICS` la instrucción para volver a crear estadísticas en el objeto. La opción **Publicar estadísticas e histogramas** también crea información de histogramas. El valor predeterminado es **No publicar estadísticas**. Para obtener más información, vea [CREATE STATISTICS &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-statistics-transact-sql).  
  
9. **Publicar opciones vardecimal** : habilita el `vardecimal` formato de tabla en la tabla de base de datos de destino cuando se habilita en la tabla de base de datos de origen. El valor predeterminado es **true**.  
  
10. **Nombres de objeto de certificado de esquema** : incluye el nombre de esquema en el nombre de los objetos que se crean. El valor predeterminado es **true**.  
  
11. **Incluir enlaces** : incluye enlaces para los objetos predeterminados y de regla en el script enviado al proveedor para su publicación. El valor predeterminado es **true**. Para obtener más información, vea [CREATE DEFAULT &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-default-transact-sql) y [CREATE RULE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-rule-transact-sql).  
  
12. **Tipos de datos que se van a publicar** : selecciona lo que se debe incluir en el script: **solo datos**, **solo esquema**o ambos. El valor predeterminado es **Esquema y datos**.  
  
 **Opciones de publicación** : especifica si se van a utilizar transacciones al publicar en el proveedor de host Web.  
  
1.  **Publicar mediante transacción** : usa transacciones al publicar en un proveedor de hospedaje Web remoto. Si la base de datos de destino no puede completar la publicación, se revierten las transacciones. El valor predeterminado es **true**.  
  
 **Opciones de tabla o vista** : las siguientes opciones solo se aplican a tablas o vistas.  
  
1.  **Publicar restricciones check** : incluye la creación de `CHECK` restricciones en el proceso de publicación. El valor predeterminado es **True**. Las restricciones `CHECK` requieren datos que se escriban en una tabla para cumplir con una condición especificada. Para más información, consulte [Unique Constraints and Check Constraints](../tables/unique-constraints-and-check-constraints.md).  
  
2.  **Publicar claves externas** : incluye la creación de claves externas en el proceso de publicación. El valor predeterminado es **true**. Las claves externas indican y exigen relaciones entre tablas. Para más información, consulte [Primary and Foreign Key Constraints](../tables/primary-and-foreign-key-constraints.md).  
  
3.  **Publicar índices de texto completo** : incluye en el script la creación de índices de texto completo. El valor predeterminado es **False**.  
  
4.  **Publicar índices** : incluye índices de tablas en el proceso de publicación. El valor predeterminado es **true**. Los índices ayudan a encontrar rápidamente los datos.  
  
5.  **Publicar claves principales** : incluye la creación de claves principales en el proceso de publicación. El valor predeterminado es **True**. Las claves principales identifican de forma exclusiva cada fila de una tabla. Para más información, consulte [Primary and Foreign Key Constraints](../tables/primary-and-foreign-key-constraints.md).  
  
6.  **Publicar desencadenadores** : incluye la creación de desencadenadores DML en el proceso de publicación. El valor predeterminado es **true**. Un desencadenador DML es una acción programada para ejecutarse cuando se produce un evento DML (lenguaje de manipulación de datos) en el servidor de base de datos. Para más información, consulte [DML Triggers](../triggers/dml-triggers.md).  
  
7.  **Publicar claves únicas** : incluye la creación de claves únicas en tablas en el proceso de publicación. Las claves únicas evitan que se especifiquen datos duplicados. El valor predeterminado es **true**. Para más información, consulte [Unique Constraints and Check Constraints](../tables/unique-constraints-and-check-constraints.md).  
  
8.  **Publicar seguimiento de cambios** : incluye el seguimiento de cambios en el proceso de publicación, si está habilitado en la base de datos de origen o en las tablas de la base de datos de origen. El valor predeterminado es **False**. Para obtener más información, vea [Acerca del seguimiento de cambios &#40;SQL Server&#41;](../track-changes/about-change-tracking-sql-server.md).  
  
9. **Publicar opciones de compresión de datos** : incluye las opciones de compresión de datos en el proceso de publicación, si están configuradas en la base de datos de origen o en las tablas de la base de datos de origen. El valor predeterminado es **true**. Para obtener más información, consulte [Data Compression](../data-compression/data-compression.md).  
  
###  <a name="ProvConfig"></a>Página configuración de proveedor  
 Use este cuadro de diálogo para ver o modificar la configuración del proveedor de hospedaje. La información de este cuadro de diálogo se puede utilizar para:  
  
-   Ver, agregar o modificar la información de conexión a un proveedor de hospedaje.  
  
-   Ver, agregar, modificar o eliminar una base de datos para una conexión de proveedor.  
  
-   Configurar automáticamente las bases de datos para un proveedor de hospedaje.  
  
 Un proveedor de hospedaje especifica la información de conexión para un servicio web que se haya creado con el proyecto Database Publishing Services en SQL Server Hosting Toolkit en CodePlex.  
  
 **Name** : nombre del proveedor de hospedaje.  
  
 **Dirección del servicio Web** : dirección https del servicio de hospedaje.  
  
 **Autenticación de servicio Web** : el nombre de usuario y la contraseña necesarios para iniciar sesión en el servicio de hospedaje.  
  
 **Guardar contraseña** : Cifre y guarde la contraseña en el equipo local.  
  
 **Bases de datos disponibles** : las bases de datos que están configuradas para proveedores de hospedaje se muestran en orden ascendente en el formato: *SERVER_NAME*. *database_name*.  
  
 **Nuevo** : abre el cuadro de diálogo Configuración de **base de datos** y agrega una nueva base de datos.  
  
 **Editar** : abre el cuadro de diálogo Configuración de **base** de datos de la base de datos seleccionada.  
  
 **Eliminar** : elimina la base de datos seleccionada.  
  
 **Establecer como predeterminado** : seleccione la base de datos como predeterminada.  
  
 **Aceptar** : guarda todos los cambios realizados en este cuadro de diálogo y vuelve al asistente.  
  
 **Cancelar** : deshacer todos los cambios realizados en este cuadro de diálogo y volver al asistente.  
  
###  <a name="Summary"></a> Página Resumen  
 En esta página se resumen las opciones que ha seleccionado en este asistente. Para cambiar una opción, haga clic en **Anterior**. Para empezar a generar los scripts que se guardarán o publicarán, haga clic en **Siguiente**.  
  
 **Revisar las selecciones** : muestra las selecciones realizadas para cada página del asistente. Expanda un nodo para ver las opciones seleccionadas de la página correspondiente.  
  
###  <a name="SavePubScripts"></a>Página guardar o publicar scripts  
 Use esta página para supervisar el progreso del asistente a medida que se produce.  
  
 **Detalles** : vea la columna **acción** para ver el progreso del asistente. Después de generar los scripts, el asistente los guarda en un archivo o los usa para publicar en un servicio web, según las selecciones. Cuando cada uno de estos pasos se haya completado, haga clic en el valor de la columna **Resultado** para ver el resultado del paso correspondiente.  
  
 **Guardar Informe** : haga clic para guardar los resultados del progreso del asistente en un archivo.  
  
 **Cancelar** : haga clic para cerrar el asistente antes de que se haya completado el procesamiento o si se produce un error.  
  
 **Finalizar** : haga clic para cerrar el asistente después de que se haya completado el procesamiento o si se produce un error.  
  
## <a name="see-also"></a>Consulte también  
 [Instalación de SMO](../server-management-objects-smo/installing-smo.md)   
 [Copiar bases de datos en otros servidores](../databases/copy-databases-to-other-servers.md)  
  
  
