---
title: Novedades de SSMA para el acceso (AccessToSQL) Microsoft Docs
authors: HJToland3;nahk-ivanov
ms.prod: sql
ms.custom: ''
ms.date: 4/2/2020
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: a24d3fc0-6911-4bfa-828a-197abf222e02
ms.author: jtoland;alexiva
ms.openlocfilehash: 2fd3da31e6a635a65f3d2a2f75320dd0586159d9
ms.sourcegitcommit: d818a307725983c921987749915fe1a381233d98
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/03/2020
ms.locfileid: "80625582"
---
# <a name="whats-new-in-ssma-for-access-accesstosql"></a>Novedades de SSMA para el acceso (AccessToSQL)

En este artículo se enumeran los cambios de SQL Server MIGRATION Assistant (SSMA) para Access en cada versión.

## <a name="ssma-v88"></a>SSMA v8.8

La versión v8.8 de SSMA for Access incluye:

* Mejoras en la estabilidad de sincronización de objetos de SQL Server
* Mejoras en el rendimiento de la interfaz gráfica de usuario durante la evaluación y la conversión
* Nuevo analizador de sintaxis de acceso para mejorar aún más el rendimiento de la conversión

## <a name="ssma-v87"></a>SSMA v8.7

La versión v8.7 de SSMA `IIF` para Access ha mejorado la conversión de funciones en consultas, así como correcciones menores y mejoras de rendimiento en la interfaz gráfica de usuario.

> [!IMPORTANT]
> Con SSMA v8.5 y versiones posteriores, .NET 4.7.2 es un requisito previo de instalación. Si necesita instalar esta versión, puede descargar el archivo en tiempo de ejecución desde [aquí.](https://dotnet.microsoft.com/download/dotnet-framework/net472)

## <a name="ssma-v86"></a>SSMA v8.6

Además de un conjunto de correcciones de destino diseñado para mejorar la facilidad de uso y el rendimiento, la versión v8.6 de SSMA para Access se ha mejorado agregando una configuración que permite a los usuarios omitir las propiedades extendidas de SSMA en el código convertido.

Para aprovechar esta configuración, en SSMA para Access, vaya a**Project Settings** >  **Conversión** > **general** > **Conversion**de configuración de proyecto de herramientas y, a continuación, en **Varios**, actualice el valor de la configuración **Omitir propiedades extendidas** a **Sí**.

![Omitir configuración de propiedades extendidas](../access/media/ssma-omit-extended-properties.png)

> [!IMPORTANT]
> Con SSMA v8.5 y versiones posteriores, .NET 4.7.2 es un requisito previo de instalación. Si necesita instalar esta versión, puede descargar el archivo en tiempo de ejecución desde [aquí.](https://dotnet.microsoft.com/download/dotnet-framework/net472)

## <a name="ssma-v85"></a>SSMA v8.5

La versión v8.5 de SSMA para Access se ha mejorado con compatibilidad con la autenticación de Azure Active Directory y compatibilidad básica con características JSON en SQL Server, junto con un conjunto específico de correcciones diseñadas para mejorar la facilidad de uso y el rendimiento.

Además, SSMA for Access ahora admite`ISNULL` `IIF`la conversión de varias funciones estándar ( , , etc.).

> [!IMPORTANT]
> Con SSMA v8.5, .NET 4.7.2 es un requisito previo de instalación. Si necesita instalar esta versión, puede descargar el archivo en tiempo de ejecución desde [aquí.](https://dotnet.microsoft.com/download/dotnet-framework/net472)

## <a name="ssma-v84"></a>SSMA v8.4

La versión v8.4 de SSMA para Access se mejora con correcciones de destino que están diseñadas para solucionar problemas de accesibilidad y corregir un error relacionado con las columnas de índice máximo (para permitir 32 en lugar de 16) para SQL Server 2016 y versiones posteriores.

> [!IMPORTANT]
> Con las versiones 7.4 de SSMA a 8.4, .NET 4.5.2 es un requisito previo de instalación.

## <a name="ssma-v83"></a>SSMA v8.3

La versión v8.3 de SSMA para Access se mejora con correcciones dirigidas diseñadas para mejorar la calidad y las métricas de conversión. Además, esta versión de SSMA para el acceso proporciona las correcciones que:

* Abordar problemas de accesibilidad.
* Agregue compatibilidad `hierarchyid` básica para el tipo en SQL Server.

## <a name="ssma-v82"></a>SSMA v8.2

La versión v8.2 de SSMA para Access se mejora con correcciones dirigidas diseñadas para mejorar la calidad y las métricas de conversión.

> [!NOTE]
> Un problema conocido con la actualización automática puede provocar el error de una actualización de SSMA v8.1 a v8.2. Si encuentra este error, descargue la nueva versión e instálela manualmente.

## <a name="ssma-v81"></a>SSMA v8.1

La versión v8.1 de SSMA para Access se mejora con correcciones dirigidas diseñadas para mejorar la calidad y las métricas de conversión.

> [!NOTE]
> Un problema conocido con la actualización automática puede provocar el error de una actualización de SSMA v8.0 a v8.1. Si encuentra este error, descargue la nueva versión e instálela manualmente.

## <a name="ssma-v80"></a>SSMA v8.0

La versión v8.0 de SSMA para Access se mejora con correcciones dirigidas diseñadas para mejorar la calidad y las métricas de conversión. Esta versión también ofrece las siguientes características nuevas:

* Compatibilidad con **instancias administradas de Azure SQL Database** como destino. Ahora puede crear nuevos proyectos destinados a Instancia administrada de Azure SQL Database:

  ![Proyecto SQL DB MI](../media/ssma-newproject-sqldbmi.png)

* Asesor **fixdena**posterior a la conversión . Más información [aquí](https://techcommunity.microsoft.com/t5/Microsoft-Data-Migration/Accelerate-your-Oracle-migrations-with-new-machine-learning/ba-p/368733).

* Selección preliminar de base de datos/esquema.

    Al conectarse al origen, el usuario ahora puede seleccionar bases de datos/esquemas de interés. Seleccionar solo los esquemas que planea migrar ahorrará tiempo durante la conexión inicial y mejorará el rendimiento general de SSMA.

   ![Objetos de filtro SSMA](../media/ssma-filter-objects.png)

## <a name="ssma-v710"></a>SSMA v7.10

La versión v7.10 de SSMA para Access se ha mejorado con correcciones específicas diseñadas para proporcionar protecciones de seguridad y privacidad adicionales para cumplir los cambios en los requisitos globales.

## <a name="ssma-v79"></a>SSMA v7.9

La versión v7.9 de SSMA for Access contiene los siguientes cambios:

* Correcciones dirigidas que mejoran la calidad y las métricas de conversión.
* Compatibilidad con la línea de comandos SSMA para modificar la asignación de tipos de datos y las preferencias del proyecto.
* El cuadro de diálogo de conexión de Azure SQL Database en SSMA también se ha modificado para especificar el nombre completo del servidor. En versiones anteriores de SSMA, el prefijo de Azure SQL Database tenía que mencionarse explícitamente dentro de la configuración de proyectos.

## <a name="ssma-v78"></a>SSMA v7.8

La versión v7.8 de SSMA for Access contiene los siguientes cambios:

* Cambiar la asignación de tipos resaltada en Configuración del proyecto.
* La capacidad de los usuarios de deshabilitar la telemetría.

## <a name="ssma-v77"></a>SSMA v7.7

La versión v7.7 de SSMA for Access contiene los siguientes cambios:

* Correcciones dirigidas que mejoran la calidad y las métricas de conversión.
* En función de la demanda popular, la versión de 32 bits de SSMA para Access está de vuelta. En comparación con la implementación anterior (antes de v7.4), hay dos paquetes de instalación, pero no se pueden instalar en paralelo. Como resultado, debe elegir la versión más adecuada en función de los componentes de conectividad que tenga. Siempre es preferible utilizar la versión de 64 bits, si es posible.

## <a name="ssma-v76"></a>SSMA v7.6

La versión v7.6 de SSMA para Access se mejora con correcciones dirigidas que mejoran la calidad y las métricas de conversión y con compatibilidad con SQL Server 2017 (versión preliminar pública). La compatibilidad con SQL Server 2017 en Windows y Linux está en versión preliminar pública y no debe usarse para las migraciones de producción.

## <a name="ssma-v75"></a>SSMA v7.5

La versión v7.5 de SSMA for Access se ha mejorado con varias mejoras para garantizar una mayor accesibilidad para las personas con discapacidades.

## <a name="ssma-v74"></a>SSMA v7.4

La versión v7.4 de SSMA for Access contiene los siguientes cambios:

* La opción Tiempo de **espera** de consulta ahora está disponible durante la detección de objetos de esquema en el origen y el destino.

  ![opción de tiempo de espera de consulta](../media/query-timeout_red.png)

* La métrica de calidad y conversión se ha mejorado con correcciones específicas, en función de los comentarios de los clientes.

  > [!IMPORTANT]
  > .NET 4.5.2 es un requisito previo para instalar SSMA v7.4. Además, a partir de v7.4, se ha interrumpido la versión de 32 bits de SSMA.

## <a name="ssma-v73"></a>SSMA v7.3

La versión v7.3 de SSMA for Access contiene los siguientes cambios:

* Métrica de calidad y conversión mejorada con correcciones específicas basadas en los comentarios de los clientes.
* Marco de extensibilidad SSMA expuesto a través de los siguientes elementos:
  * Exportar funcionalidad a un proyecto de SQL Server Data Tools (SSDT)SQL Server Data Tools (SSDT).
    * Ahora puede exportar scripts de esquema de SSMA a un proyecto SSDT. Puede usar los scripts de esquema para realizar cambios de esquema adicionales e implementar la base de datos.

        ![Guardar como comando de proyecto SSDT](../media/export-schema-scripts_red.png)
  * Bibliotecas que SSMA puede consumir para realizar conversiones personalizadas.
    * Ahora puede construir código que puede controlar las conversiones de sintaxis personalizadas y las conversiones que no se controlaban anteriormente por SSMA.
      * Las instrucciones sobre cómo construir un convertidor personalizado, junto con un proyecto de ejemplo para la conversión, están disponibles en la entrada de blog [Extending SQL Server Migration Assistant's conversion capabilities](https://techcommunity.microsoft.com/t5/Microsoft-Data-Migration/Extending-SQL-Server-Migration-Assistant-s-conversion/ba-p/1004181).

## <a name="ssma-v72"></a>SSMA v7.2

La versión v7.2 de SSMA for Access contiene los siguientes cambios:

* Métrica de calidad y conversión mejorada con correcciones específicas basadas en los comentarios de los clientes.
* Mejoras de telemetría para proporcionar mejores puntos de datos para solucionar problemas de los clientes y mejorar las tasas de conversión de SSMA.

## <a name="ssma-v71"></a>SSMA v7.1

La versión v7.1 de SSMA for Access contiene los siguientes cambios:

* SQL Server 2017 en Windows y Linux CTP1 es ahora una plataforma de destino compatible para la migración. Esta característica está en versión preliminar técnica y admite el esquema y el movimiento de datos para dirigirse a los servidores SQL.
* SSMA ahora admite actualizaciones automáticas para descargar la última versión de SSMA tan pronto como esté disponible.
* Los archivos binarios instalables SSMA ahora se entregan a través de archivos de paquete de Windows Installer (.msi).

## <a name="may-2016"></a>Mayo de 2016

La versión de mayo de 2016 de SSMA for Access contiene los siguientes cambios:

* Se ha añadido compatibilidad oficial con SQL Server 2016.
* Se ha eliminado la comprobación del instalador de .NET 2.0.
* Corregido `save-project` `open-project` y comandos para la consola SSMA.
* Se `securepassword` ha corregido el comando para la consola SSMA.
* Se ha corregido el recuento de objetos para la carga inicial.
* Se ha corregido la carga de datos de tablas para las pestañas de la interfaz de usuario para Access.
* Se ha corregido un error en la configuración global.

## <a name="march-2016"></a>marzo de 2016

La versión preliminar de marzo de 2016 de SSMA para Access agrega compatibilidad para la migración a SQL Server 2016.

## <a name="january-2016"></a>Enero de 2016

La versión de mantenimiento de enero de 2016 de SSMA for Access contiene los siguientes cambios:

* Se ha corregido la función no válida para el valor predeterminado de un campo GUID (RFC 3894811).
* Se ha corregido el bloqueo al importar registros a SQL Database (Azure) (RFC 4919573).
* Se ha añadido el elemento de menú Ver registro a SSMA (RFC 5706203).
* Se ha añadido telemetría.

## <a name="july-2014"></a>Julio de 2014

La versión de julio de 2014 de SSMA for Access contiene los siguientes cambios:

* Se ha mejorado la conversión de código de azure SQL DB.
* Se ha movido la funcionalidad del paquete de extensión al esquema para admitir Azure SQL DB.
* Mejoras de rendimiento probadas para bases de datos con más de 10k objetos.
* Se han añadido mejoras en la interfaz de usuario para tratar con un gran número de objetos.
* Se ha añadido compatibilidad para resaltar esquemas LOB "bien conocidos" (para que se puedan ignorar en la conversión).
* Se han añadido mejoras en la velocidad de conversión.
* Se ha añadido compatibilidad para mostrar los recuentos de objetos en la interfaz de usuario.
* Se ha reducido el tamaño del informe en más de un 25%.
* Mensajes de error mejorados para construcciones sin analizar.

## <a name="april-2014"></a>Abril de 2014

La versión de abril de 2014 de SSMA for Access contiene los siguientes cambios:

* Se ha agregado compatibilidad con MS SQL Server 2014.
* Se han corregido errores relacionados con la conversión a Azure.
* Se han corregido errores relacionados con páginas de informes invisibles en IE 10.

## <a name="january-2012"></a>enero de 2012

La versión de enero de 2012 de SSMA for Access contiene los siguientes cambios:

* Se ha proporcionado la opción de no conservar el nombre de usuario y la contraseña de las tablas vinculadas de MS Access después de la migración.
* Establezca acciones en cascada para referencias circulares en Sin acción.
* Se han establecido los mensajes adecuados que indican acciones en cascada para referencias circulares en Sin acción.

## <a name="july-2011"></a>julio de 2011

La versión de julio de 2011 de SSMA para Access agrega informes de errores mejorados durante la migración de datos.

## <a name="april-2011"></a>Abril de 2011

La versión de abril de 2011 de SSMA for Access contiene los siguientes cambios:

* Se ha añadido una única instalación de "SSMA for Access", que admite [!INCLUDE [ssVersion2005](../../includes/ssversion2005-md.md)], [!INCLUDE [ssSQL10](../../includes/sssql10-md.md)], [!INCLUDE [ssSQL11](../../includes/sssql11-md.md)] y Azure SQL.
* Se ha añadido [!INCLUDE [ssSQL11](../../includes/sssql11-md.md)]la posibilidad de conectarse a .
* Se ha agregado Compatibilidad con SSMA para la versión de la consola de acceso para la compatibilidad con versiones anteriores. Puede abrir los proyectos creados por versiones anteriores a SSMA v5.0.
* Se ha añadido la capacidad de instalar sSMA v5.0 producto lado a lado (SxS) con versiones anteriores del producto SSMA.

## <a name="july-2010"></a>Julio de 2010

La versión de julio de 2010 de SSMA for Access contiene los siguientes cambios:

* Se ha agregado compatibilidad para migrar a SQL Server 2008 R2 y Azure SQL.
* Se ha agregado una conexión segura a SQL Server y Azure SQL.
* Se ha añadido compatibilidad con bases de datos de Access 2010.
* Se ha añadido una nueva aplicación de consola SSMA para la ejecución de la línea de comandos.
* Se ha agregado `DateTime2` compatibilidad con el tipo de datos de SQL ServerSQL Server .

## <a name="june-2008"></a>Junio de 2008

La versión de junio de 2008 de SSMA for Access agrega compatibilidad con bases de datos de Access 2007.

## <a name="may-2007"></a>Mayo de 2007

La versión de mayo de 2007 de SSMA for Access contiene los siguientes cambios:

* Se ha agregado compatibilidad con bases de datos de Access que usan directivas de grupo de trabajo.
* Proporciona la capacidad de eliminar objetos convertidos desde el explorador de metadatos de SQL ServerSQL Server .
* Se ha agregado compatibilidad con comentarios introducidos por el usuario en el modo SQL con formato de SQL ServerSQL Server .
* Se han añadido mejoras en la conversión de objetos.

## <a name="november-2006"></a>Noviembre de 2006

La versión de noviembre de 2006 de SSMA for Access contiene los siguientes cambios:

* Se ha añadido un nuevo Asistente para migración de [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)]bases de datos que le guía a través de la migración de una sola base de datos de Access a .
* Se ha añadido un nuevo comando Convertir, Cargar y Migrar [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)]que convierte las [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)] bases de datos de Access, carga los objetos convertidos en y migra los datos a todos en un solo paso.
* Se ha mejorado la migración de consultas. La migración de consultas ahora convierte más consultas SELECT en vistas. Para obtener más información, consulte [Conversión de objetos](converting-access-database-objects-accesstosql.md)de base de datos de acceso .
* Se ha añadido la capacidad de [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)] editar las propiedades de tabla e índice en la pestaña **Tabla.**
* Se han añadido nuevos ajustes globales:
  * Puede optar por mostrar números de línea en las ventanas del editor.
  * Puede configurar SSMA para solicitar que reemplace los objetos duplicados, o siempre o nunca reemplazar objetos duplicados durante la conversión de esquema.
* Se ha agregado una nueva opción de conversión que le permite especificar si SSMA muestra una advertencia cuando una consulta compleja contiene un comodín.

## <a name="july-2006"></a>Julio de 2006

La versión de julio de 2006 de SSMA for Access fue la versión inicial.
