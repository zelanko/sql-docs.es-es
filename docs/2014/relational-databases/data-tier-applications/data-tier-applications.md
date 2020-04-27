---
title: Aplicaciones de capa de datos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- designing DACs
- How to [DAC]
- data-tier application [SQL Server], designing
- wizard [DAC]
ms.assetid: a04a2aba-d07a-4423-ab8a-0a31658f6317
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b9731a25633b5bc127039ae81a31df8c69bb8ccb
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "62873106"
---
# <a name="data-tier-applications"></a>Aplicaciones de capa de datos
  Una aplicación de capa de datos (DAC) es una entidad de administración de bases de datos lógicas que define todos los objetos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] asociados a una base de datos de usuario, como tablas, vistas y objetos de instancia, incluidos los inicios de sesión. Una DAC es una unidad independiente de implementación de bases de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que permite a los desarrolladores y los administradores de bases de datos en el nivel de capa de datos empaquetar objetos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en un artefacto portátil denominado paquete DAC y también conocido como DACPAC.  
  
 Un BACPAC es un artefacto relacionado que encapsula el esquema de la base de datos junto con los datos almacenados en la base de datos.  
  
## <a name="benefits-of-data-tier-applications"></a>Ventajas de las aplicaciones de capa de datos  
 El ciclo de vida de la mayoría de las aplicaciones de base de datos implica a los desarrolladores y administradores de bases de datos (DBA) que comparten e intercambian scripts y notas de integración ad hoc para las actividades de actualización y mantenimiento de aplicaciones. Aunque esto es aceptable para un pequeño número de bases de datos, deja de ser rápidamente escalable una vez que las bases de datos aumentan en número, tamaño y complejidad.  
  
 Un DAC es una herramienta de productividad y administración del ciclo de vida de las bases de datos que permite el desarrollo declarativo de las mismas para simplificar la implementación y la administración. Un desarrollador puede crear una base de datos en un proyecto de base de datos de herramientas de datos de SQL Server y generar después la base de datos en un DACPAC para la entrega a un DBA. El DBA puede implementar la DAC utilizando SQL Server Management Studio para una instancia de producción o de pruebas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]. También puede utilizar el DACPAC para actualizar una base de datos implementada anteriormente mediante SQL Server Management Studio. Para completar el ciclo de vida, el DBA puede extraer la base de datos en un DACPAC y entregarla a un desarrollador para que refleje los ajustes de producción de o pruebas o para que habilite los cambios de diseño de base de datos posteriores en respuesta a los cambios de la aplicación.  
  
 La ventaja de una implementación controlada por DAC en un ejercicio controlado por script es que la herramienta ayuda al DBA identificar y validar los comportamientos de bases de datos de origen y destino diferentes. Durante las actualizaciones, la herramienta advierte al DBA cuando la actualización puede provocar una pérdida de datos y también proporciona un plan de actualización. El DBA puede evaluar el plan y utilizar luego la herramienta para continuar con la actualización.  
  
 Las DAC también admiten el control de versiones para ayudar al desarrollador y al DBA a mantener y administrar el linaje de las bases de datos durante su ciclo de vida.  
  
## <a name="dac-concepts"></a>Conceptos de DAC  
 Una DAC simplifica el desarrollo, la implementación y la administración de elementos de capa de datos que admiten una aplicación:  
  
-   Una aplicación de capa de datos (DAC) es una entidad de administración de bases de datos lógicas que define todos los objetos de SQL Server como tablas, vistas y objetos de instancia, asociados a una base de datos de usuario. Es una unidad independiente de implementación de bases de datos de SQL Server que permite a los desarrolladores y los administradores de bases de datos en el nivel de capa de datos empaquetar objetos de SQL Server en un artefacto portátil denominado paquete DAC o archivo .dacpac.  
  
-   Para que una base de datos de SQL Server sea tratada como una DAC, debe estar registrada, ya sea de forma explícita mediante una operación de usuario, o bien de forma implícita mediante una de las operaciones de DAC. Cuando se registra una base de datos, la versión de DAC y otras propiedades se registran como parte de los metadatos de la base de datos. A la inversa, también es posible no registrar una base de datos que esté sin sus propiedades de DAC.  
  
-   En general, las herramientas de DAC pueden leer archivos DACPAC generados por herramientas de DAC en versiones anteriores de SQL Server y también pueden implementar DACPAC en versiones anteriores de SQL Server. Sin embargo, las herramientas de DAC de versiones anteriores no pueden leer archivos de DACPAC generados por herramientas de DAC en versiones posteriores. Concretamente:  
  
    -   Las operaciones DAC se introdujeron en SQL Server 2008 R2. Además de las bases de datos de SQL Server 2008 R2, las herramientas admiten la generación de archivos de DACPAC de bases de datos de SQL Server 2008, SQL Server 2005 y SQL Server 2000.  
  
    -   Además de las bases de datos de [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] , las herramientas proporcionadas con [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] pueden leer archivos de DACPAC generados por las herramientas de DAC proporcionadas con SQL Server 2008 R2 o SQL Server 2012. Esto incluye las bases de datos de SQL Server 2012, SQL Server 2008 R2, SQL Server 2008 y SQL Server 2005, pero no las de SQL Server 2000.  
  
    -   Las herramientas de DAC de SQL Server 2008 R2 no pueden leer archivos de DACPAC generados por las herramientas de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ni  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
-   Un DACPAC es un archivo de Windows con una extensión .dacpac. El archivo admite un formato abierto que consta de varias secciones XML que representan detalles del origen de DACPAC, los objetos de la base de datos y otras características. Un usuario experto puede desempaquetar el archivo mediante la utilidad DacUnpack.exe que se proporciona con el producto para inspeccionar cada sección de forma más minuciosa.  
  
-   El usuario debe ser miembro del rol dbmanager o tener asignados permisos CREATE DATABASE para crear una base de datos, incluida la creación de una base de datos para implementar un paquete DAC. El usuario debe ser miembro del rol dbmanager, o tener asignados permisos DROP DATABASE para quitar una base de datos.  
  
## <a name="dac-tools"></a>Herramientas de DAC  
 Un DACPAC se puede utilizar sin problemas con las herramientas que se proporcionan con [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Estas herramientas abordan los requisitos de los diferentes usuarios que utilizan un DACPAC como unidad de interoperabilidad.  
  
-   Desarrollador de aplicaciones  
  
    -   Un desarrollador de bases de datos puede utilizar un proyecto de base de datos de herramientas de datos de SQL Server para diseñar una base de datos. Una compilación correcta de este proyecto da como resultado la generación de un DACPAC contenido en un archivo .dacpac.  
  
    -   Además, el desarrollador puede importar un DACPAC en un proyecto de base de datos y continuar diseñando la base de datos.  
  
    -   Las herramientas de SQL Server también admiten base de datos local para el desarrollo de aplicaciones de bases de datos de lado cliente no conectadas. El desarrollador puede utilizar una instantánea de esta base de datos local para crear un DACPAC contenido en un archivo .dacpac.  
  
    -   Independientemente, el desarrollador puede publicar un proyecto de base de datos directamente en una base de datos sin tener que generar un DACPAC. La operación de publicación sigue un comportamiento similar a la operación de implementación con otras herramientas.  
  
-   Administrador de base de datos  
  
    -   Un administrador de base de datos puede utilizar SQL Server Management Studio para extraer un DACPAC de una base de datos existente y para realizar otras operaciones DAC.  
  
    -   Además, el administrador de una base de datos de [!INCLUDE[ssSDS](../../includes/sssds-md.md)] puede utilizar el portal de administración de SQL Azure para las operaciones DAC.  
  
-   Proveedor independiente de software  
  
    -   Los servicios de hospedaje y otros productos de administración de datos de SQL Server pueden utilizar la API de DACFx para las operaciones DAC.  
  
-   Administrador de TI  
  
    -   Los integradores y administradores de sistemas de TI pueden utilizar la herramienta de línea de comandos SqlPackage.exe para las operaciones DAC.  
  
## <a name="dac-operations"></a>Operaciones DAC  
 Un DAC admite las siguientes operaciones:  
  
-   **EXTRACT**: el usuario puede extraer una base de datos en un DACPAC.  
  
-   **DEPLOY**: el usuario puede implementar un DACPAC en un servidor de host. Cuando la implementación se realiza con una herramienta de administración como SQL Server Management Studio o el portal de administración de SQL Azure, la base de datos resultante en el servidor de host se registra implícitamente como una aplicación de capa de datos.  
  
-   **REGISTER**: el usuario puede registrar una base de datos como una aplicación de capa de datos.  
  
-   **UNREGISTER**: se puede anular del registro una base de datos registrada anteriormente como DAC.  
  
-   **UPGRADE**: se puede actualizar una base de datos mediante un DACPAC. La actualización se admite incluso en las bases de datos no registradas previamente como aplicaciones de capa de datos, pero como resultado de la actualización, la base de datos se registrará implícitamente.  
  
## <a name="backup-package-bacpac"></a>Paquete de copia de seguridad (.bacpac)  
 Un BACPAC es un artefacto que encapsula el esquema de la base de datos junto con los datos almacenados en la base de datos. El BACPAC es un archivo de Windows con una extensión .bacpac. Similar al DACPAC, el formato de archivo BACPAC es abierto: el contenido del esquema del BACPAC es idéntico al del DACPAC. Los datos se almacenan en formato JSON.  
  
 DACPAC y BACPAC son similares pero se dirigen a escenarios diferentes. Un DACPAC está dirigido a la captura y la implementación del esquema, incluida la actualización de una base de datos existente. El caso de uso principal de un DACPAC es implementar un esquema estrictamente definido en entornos de desarrollo, prueba y producción, y a la inversa: capturar el esquema de producción y volver a aplicarlo a los entornos de prueba y desarrollo.  
  
 Por otro lado, un BACPAC está dirigido a capturar el esquema y los datos. Un BACPAC es el equivalente lógico de una copia de seguridad de base de datos y no se puede utilizar para actualizar las bases de datos existentes. El caso de uso principal de un BACPAC es mover una base de datos de un servidor a otro, o de un servidor local a la nube, y almacenar una base de datos existente en un formato abierto.  
  
 Un BACPAC admite dos operaciones principales:  
  
-   **EXPORT**: el usuario puede exportar el esquema y los datos de una base de datos a un BACPAC.  
  
-   **IMPORT**: el usuario puede importar el esquema y los datos a una base de datos nueva en el servidor de host.  
  
 Ambas funciones son compatibles con las herramientas de administración de bases de datos: Server Management Studio, Portal de administración de SQL Azure y API de DACFx.  
  
## <a name="permissions"></a>Permisos  
 Es necesario ser miembro del rol `dbmanager` o tener asignados permisos `CREATE DATABASE` para crear una base de datos, incluida la creación de una base de datos para implementar un paquete DAC. Es necesario ser miembro del rol `dbmanager` o tener asignados permisos `DROP DATABASE` para quitar una base de datos.  
  
## <a name="data-tier-application-tasks"></a>Tareas de la aplicación de capa de datos  
  
|Descripción de la tarea|Tema|  
|----------------------|-----------|  
|Describe cómo usar un archivo de paquete DAC para crear una nueva instancia de DAC.|[Implementar una aplicación de capa de datos](deploy-a-data-tier-application.md)|  
|Describe cómo usar un archivo de paquete DAC para actualizar una instancia a una nueva versión de la DAC.|[Actualizar una aplicación de capa de datos](upgrade-a-data-tier-application.md)|  
|Describe cómo quitar una instancia de DAC. Puede elegir también separar o quitar la base de datos asociada o dejar la base de datos intacta.|[Eliminar una aplicación de capa de datos](delete-a-data-tier-application.md)|  
|Describe cómo ver estados de DAC actualmente implementados mediante la utilidad de SQL Server.|[Supervisar aplicaciones de capa de datos](data-tier-applications.md)|  
|Describe cómo crear un archivo de .bacpac que contiene un archivo de datos y metadatos de la DAC.|[Exportar una aplicación de capa de datos](export-a-data-tier-application.md)|  
|Describe cómo usar un archivo de almacenamiento de DAC (.bacpac) para realizar una restauración lógica de DAC, o migrar DAC a otra instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)] o [!INCLUDE[ssSDS](../../includes/sssds-md.md)].|[Importar un archivo de bacpac para crear una nueva base de datos de usuario](import-a-bacpac-file-to-create-a-new-user-database.md)|  
|Describe cómo importar un archivo BACPAC para crear una base de datos de usuario en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|[Extraer una DAC de una base de datos](extract-a-dac-from-a-database.md)|  
|Describe cómo promover una base de datos existente para que sea una instancia de DAC. La definición de DAC está compilada y almacenada en las bases de datos del sistema.|[Registrar una base de datos como una DAC](register-a-database-as-a-dac.md)|  
|Describe cómo consultar el contenido de un paquete DAC y las acciones que una actualización de DAC realizará antes de usar el paquete en un sistema de producción.|[Validar un paquete DAC](validate-a-dac-package.md)|  
|Describe cómo colocar el contenido de un paquete DAC en una carpeta donde un administrador de bases de datos puede revisar lo que hace la DAC antes de implementarlo en un servidor de producción.|[Desempaquetar un paquete de DAC](unpack-a-dac-package.md)|  
|Describe cómo usar un asistente para implementar una base de datos existente. El asistente usa DAC para realizar la implementación.|[Implementar una base de datos mediante una DAC](deploy-a-database-by-using-a-dac.md)|  
  
## <a name="see-also"></a>Consulte también  
 [Compatibilidad de DAC con las versiones y objetos de SQL Server](dac-support-for-sql-server-objects-and-versions.md)  
  
  
