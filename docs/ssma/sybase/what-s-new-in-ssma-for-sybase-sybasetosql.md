---
title: Novedades de SSMA para SAP ASE (SybaseToSQL) Microsoft Docs
authors: HJToland3;nahk-ivanov
ms.prod: sql
ms.custom: ''
ms.date: 4/2/2020
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 2be0cf8d-6dbe-443a-abbd-036249922205
ms.author: jtoland;alexiva
ms.openlocfilehash: 7f23c7e1c676b4ade42b43cf963e0fa6956f93c6
ms.sourcegitcommit: d818a307725983c921987749915fe1a381233d98
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/03/2020
ms.locfileid: "80625595"
---
# <a name="whats-new-in-ssma-for-sap-ase-sybasetosql"></a>Novedades de SSMA para SAP ASE (SybaseToSQL)

En este artículo se enumeran los cambios de SQL Server Migration Assistant (SSMA) para SAP ASE (anteriormente SSMA para Sybase) en cada versión.

## <a name="ssma-v88"></a>SSMA v8.8

La versión v8.8 de SSMA para SAP ASE incluye:

* Mejoras en la estabilidad de sincronización de objetos de SQL Server
* Mejoras en el rendimiento de la interfaz gráfica de usuario durante la evaluación y la conversión
* Se ha corregido el problema con la falta de caracteres en las definiciones SQL de los objetos

## <a name="ssma-v87"></a>SSMA v8.7

La versión v8.7 de SSMA para SAP ASE tiene correcciones menores y mejoras de rendimiento en la interfaz gráfica de usuario.

> [!IMPORTANT]
> Con SSMA v8.5 y versiones posteriores, .NET 4.7.2 es un requisito previo de instalación. Si necesita instalar esta versión, puede descargar el archivo en tiempo de ejecución desde [aquí.](https://dotnet.microsoft.com/download/dotnet-framework/net472)

## <a name="ssma-v86"></a>SSMA v8.6

Además de un conjunto específico de correcciones diseñadas para mejorar la facilidad de uso y el rendimiento, la versión v8.6 de SSMA para SAP ASE se ha mejorado agregando una configuración que permite a los usuarios omitir las propiedades extendidas de SSMA en el código convertido.

Para aprovechar esta configuración, en**Project Settings** > SSMA para SAP ASE, vaya **a** > **Conversión****general** > de configuración de proyecto de herramientas y, a continuación, en **Varios**, actualice el valor de la configuración **Omitir propiedades extendidas** a **Sí**.

![Omitir configuración de propiedades extendidas](../sybase/media/ssma-omit-extended-properties.png)

> [!IMPORTANT]
> Con SSMA v8.5 y versiones posteriores, .NET 4.7.2 es un requisito previo de instalación. Si necesita instalar esta versión, puede descargar el archivo en tiempo de ejecución desde [aquí.](https://dotnet.microsoft.com/download/dotnet-framework/net472)

## <a name="ssma-v85"></a>SSMA v8.5

La versión v8.5 de SSMA para SAP ASE se ha mejorado con compatibilidad con la autenticación de Azure Active Directory y compatibilidad básica con características JSON en SQL Server, junto con un conjunto específico de correcciones diseñadas para mejorar la facilidad de uso y el rendimiento.

Además, SSMA para SAP ASE ahora le permite ocultar tablas y vistas del sistema (excluirlas de la conversión).

> [!IMPORTANT]
> Con SSMA v8.5, .NET 4.7.2 es un requisito previo de instalación. Si necesita instalar esta versión, puede descargar el archivo en tiempo de ejecución desde [aquí.](https://dotnet.microsoft.com/download/dotnet-framework/net472)

## <a name="ssma-v84"></a>SSMA v8.4

La versión v8.4 de SSMA para SAP ASE se ha mejorado con correcciones de destino diseñadas para solucionar problemas de accesibilidad y corregir un error relacionado con las columnas de índice máximo (para permitir 32 en lugar de 16) para SQL Server 2016 y versiones posteriores.

> [!IMPORTANT]
> Con las versiones 7.4 a 8.4 de SSMA, .NET 4.5.2 es un requisito previo de instalación.

## <a name="ssma-v83"></a>SSMA v8.3

La versión v8.3 de SSMA para SAP ASE se ha mejorado con correcciones específicas diseñadas para mejorar la calidad y las métricas de conversión. Además, esta versión de SSMA para SAP ASE proporciona arreglos que:

* Abordar problemas de accesibilidad
* Agregar compatibilidad `hierarchyid` básica para el tipo en SQL Server

## <a name="ssma-v82"></a>SSMA v8.2

La versión v8.2 de SSMA para SAP ASE se ha mejorado con un conjunto específico de correcciones diseñadas para mejorar las métricas de calidad y conversión, así como correcciones para:

* Un problema con índices no agrupados deshabilitados después de la migración de datos.
* Detección de .NET Framework durante la instalación silenciosa.
* Un bloqueo intermitente que se produce cuando se descarga una nueva versión.

> [!NOTE]
> Un problema conocido con la actualización automática puede provocar el error de una actualización de SSMA v8.1 a v8.2. Si encuentra este error, descargue la nueva versión e instálela manualmente.

## <a name="ssma-v81"></a>SSMA v8.1

La versión v8.1 de SSMA para SAP ASE se ha mejorado con correcciones específicas diseñadas para mejorar la calidad y las métricas de conversión.

> [!NOTE]
> Un problema conocido con la actualización automática puede provocar el error de una actualización de SSMA v8.0 a v8.1. Si encuentra este error, descargue la nueva versión e instálela manualmente.

## <a name="ssma-v80"></a>SSMA v8.0

La versión v8.0 de SSMA para SAP ASE se ha mejorado con correcciones específicas diseñadas para mejorar la calidad y las métricas de conversión. Además, esta versión ofrece las siguientes características nuevas:

* Compatibilidad con **instancias administradas de Azure SQL Database** como destino. Ahora puede crear nuevos proyectos destinados a Instancia administrada de Azure SQL Database:

  ![Proyecto SQL DB MI](../media/ssma-newproject-sqldbmi.png)

* Asesor **fixdena**posterior a la conversión . Más información [aquí](https://blogs.msdn.microsoft.com/datamigration/2019/02/17/%20accelerate-your-oracle-migrations-with-new-machine-learning-capabilities-in-ssma/).

* Selección preliminar de base de datos/esquema.

  Al conectarse al origen, el usuario ahora puede seleccionar bases de datos/esquemas de interés. Seleccionar solo los esquemas que planea migrar ahorrará tiempo durante la conexión inicial y mejorará el rendimiento general de SSMA.

  ![Objetos de filtro SSMA](../media/ssma-filter-objects.png)

## <a name="ssma-v710"></a>SSMA v7.10

La versión v7.10 de SSMA para SAP ASE se ha mejorado con correcciones específicas diseñadas para proporcionar protecciones de seguridad y privacidad adicionales para cumplir los cambios en los requisitos globales.

## <a name="ssma-v79"></a>SSMA v7.9

La versión v7.9 de SSMA para SAP ASE contiene los siguientes cambios:

* Correcciones dirigidas que mejoran la calidad y las métricas de conversión.
* Compatibilidad con la línea de comandos SSMA para modificar la asignación de tipos de datos y las preferencias del proyecto.
* Compatibilidad con la migración de datos mediante SQL Server Integration Services (SSIS). Después de convertir el esquema, es posible crear un paquete SSIS mediante una opción de menú contextual con el botón derecho.
* El cuadro de diálogo de conexión de Azure SQL Database en SSMA también se ha modificado para especificar el nombre completo del servidor. En versiones anteriores de SSMA, el prefijo de Azure SQL Database tenía que mencionarse explícitamente dentro de la configuración de proyectos.

## <a name="ssma-v78"></a>SSMA v7.8

La versión v7.8 de SSMA para SAP ASE contiene los siguientes cambios:

* Cambiar asignación de tipos resaltada en **Configuración del proyecto**.
* La capacidad de los usuarios de deshabilitar la telemetría.

## <a name="ssma-v77"></a>SSMA v7.7

La versión v7.7 de SSMA para SAP ASE contiene los siguientes cambios:

* SSMA para SAP ASE se ha mejorado con correcciones específicas que mejoran la calidad y las métricas de conversión.
* Según la demanda popular, la versión de 32 bits de SSMA para SAP ASE está de vuelta. En comparación con la implementación anterior (antes de v7.4), hay dos paquetes de instalación, pero no se pueden instalar en paralelo. Como resultado, debe elegir la versión más adecuada en función de los componentes de conectividad que tenga. Siempre es preferible utilizar la versión de 64 bits, si es posible.

## <a name="ssma-v76"></a>SSMA v7.6

La versión v7.6 de SSMA para SAP ASE contiene los siguientes cambios:

* Correcciones dirigidas que mejoran la calidad y las métricas de conversión y con compatibilidad con SQL Server 2017 (versión preliminar pública). La compatibilidad con SQL Server 2017 en Windows y Linux está en versión preliminar pública y no debe usarse para las migraciones de producción.
* Soporte para la conversión de funciones Sybase.

## <a name="ssma-v75"></a>SSMA v7.5

La versión v7.5 de SSMA para SAP ASE (anteriormente SSMA para Sybase) contiene los siguientes cambios:

* Varias mejoras para garantizar una mayor accesibilidad para las personas con discapacidad.
* Compatibilidad `CREATE OR REPLACE` con la sintaxis.

## <a name="ssma-v74"></a>SSMA v7.4

La versión v7.4 de SSMA para Sybase contiene los siguientes cambios:

* La opción Tiempo de **espera** de consulta ahora está disponible durante la detección de objetos de esquema en el origen y el destino.

  ![opción de tiempo de espera de consulta](../media/query-timeout_red.png)
* La métrica de calidad y conversión se ha mejorado con correcciones específicas, en función de los comentarios de los clientes.

  > [!IMPORTANT]
  > .NET 4.5.2 es un requisito previo para instalar SSMA v7.4. Además, a partir de v7.4, se está interrumpiendo la versión de 32 bits de SSMA.

## <a name="ssma-v73"></a>SSMA v7.3

La versión v7.3 de SSMA para Sybase contiene los siguientes cambios:

* Métrica de calidad y conversión mejorada con correcciones específicas basadas en los comentarios de los clientes.
* Marco de extensibilidad SSMA expuesto a través de los siguientes elementos:
  * Exportar funcionalidad a un proyecto de SQL Server Data Tools (SSDT)SQL Server Data Tools (SSDT).
    * Ahora puede exportar scripts de esquema de SSMA a un proyecto SSDT. Puede usar los scripts de esquema para realizar cambios de esquema adicionales e implementar la base de datos.

        ![Guardar como comando de proyecto SSDT](../media/export-schema-scripts_red.png)
  * Bibliotecas que SSMA puede consumir para realizar conversiones personalizadas.
    * Ahora puede construir código que puede controlar las conversiones de sintaxis personalizadas y las conversiones que no se controlaban anteriormente por SSMA.
      * Las instrucciones sobre cómo construir un convertidor personalizado están disponibles en esta entrada de blog, [Extending SQL Server Migration Assistant's conversion capabilities](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/).
      * Descargue un proyecto de ejemplo para la conversión desde esta entrada de [blog.](https://blogs.msdn.microsoft.com/datamigration/ssmafororacleconversionsample/)

## <a name="ssma-v72"></a>SSMA v7.2

La versión v7.2 de SSMA para Sybase contiene los siguientes cambios:

* Métrica de calidad y conversión mejorada con correcciones específicas basadas en los comentarios de los clientes.
* Mejoras de telemetría para proporcionar mejores puntos de datos para solucionar problemas de los clientes y mejorar las tasas de conversión de SSMA.

## <a name="ssma-v71"></a>SSMA v7.1

La versión v7.1 de SSMA para Sybase contiene los siguientes cambios:

* SQL Server 2017 en Windows y Linux CTP1 es ahora una plataforma de destino compatible para la migración. Esta característica está en versión preliminar técnica y admite el esquema y el movimiento de datos para dirigirse a los servidores SQL.
* Compatibilidad con actualizaciones automáticas para descargar la última versión de SSMA tan pronto como esté disponible.
* Los archivos binarios instalables SSMA ahora se entregan a través de archivos de paquete de Windows Installer (.msi).

## <a name="may-2016"></a>Mayo de 2016

La versión de mayo de 2016 de SSMA para Sybase contiene los siguientes cambios:

* Se ha agregado compatibilidad con SQL Server 2016.
* Se ha eliminado la comprobación del instalador de .NET 2.0.
* Se ha actualizado la dependencia del paquete de extensión de .NET 3.5 a .NET 4.0.
* Corregido `save-project` `open-project` y comandos para la consola SSMA.
* Se `securepassword` ha corregido el comando para la consola SSMA.
* Se ha corregido el recuento de objetos para la carga inicial.
* Se ha corregido un error en la configuración global.

## <a name="march-2016"></a>marzo de 2016

La versión preliminar de marzo de 2016 de SSMA para Sybase agrega compatibilidad para la migración a SQL Server 2016.

## <a name="january-2016"></a>Enero de 2016

La versión de mantenimiento de enero de 2016 de SSMA para Sybase contiene los siguientes cambios:

* Se ha añadido el elemento de menú Ver registro a SSMA (RFC 5706203).
* Se ha añadido telemetría.

## <a name="july-2014"></a>Julio de 2014

La versión de julio de 2014 de SSMA para Sybase contiene los siguientes cambios:

* Se ha mejorado la conversión de código de azure SQL DB.
* Se ha movido la funcionalidad del paquete de extensión al esquema para admitir Azure SQL DB.
* Se han añadido mejoras de rendimiento probadas para bases de datos con más de 10 k objetos.
* Se han añadido mejoras en la interfaz de usuario para tratar con un gran número de objetos.
* Se ha añadido la capacidad de resaltar esquemas LOB conocidos (para que se puedan ignorar en la conversión).
* Se han añadido mejoras en la velocidad de conversión.
* Se ha añadido la capacidad de mostrar los recuentos de objetos en la interfaz de usuario.
* Se ha reducido el tamaño del informe en más de un 25%.
* Mensajes de error mejorados para construcciones sin analizar.

## <a name="april-2014"></a>Abril de 2014

La versión de abril de 2014 de SSMA para Sybase contiene los siguientes cambios:

* Se ha agregado compatibilidad con MS SQL Server 2014.
* Se han corregido errores relacionados con la conversión a Azure.
* Se han corregido errores relacionados con las páginas de informes invisibles en IE 10.

## <a name="january-2012"></a>enero de 2012

La versión de enero de 2012 de SSMA para Sybase contiene los siguientes cambios:

* Se ha añadido compatibilidad con la conversión del desencadenador de reversión.
* Arreglo proporcionado para `@@ROWCOUNT` `@@ERROR` convertir y `SET` en la misma instrucción.

## <a name="july-2011"></a>julio de 2011

La versión de julio de 2011 de SSMA para Sybase proporciona informes de errores mejorados durante la migración de datos.

## <a name="april-2011"></a>Abril de 2011

La versión de abril de 2011 de SSMA para Sybase contiene los siguientes cambios:

* Producto consolidado "SSMA para Sybase", [!INCLUDE [ssSQL10](../../includes/sssql10-md.md)] [!INCLUDE [ssSQL11](../../includes/ssSQL11-md.md)] que admite [!INCLUDE [ssVersion2005](../../includes/ssversion2005-md.md)], y Azure SQL.
* Se ha añadido compatibilidad [!INCLUDE [ssSQL11](../../includes/sssql11-md.md)]para conectar y migrar a .
* Se ha añadido una nueva característica para convertir y migrar bases de datos Sybase a Azure SQL.
* Motor de migración de datos del lado cliente mejorado, que admite la migración paralela de datos.
* Mejora del rendimiento de la migración de datos con modelos de recuperación de registrosimple y masivo.
* Se ha añadido la capacidad de convertir y migrar correctamente bases de datos Sybase que distinguen mayúsculas de minúsculas a SQL Server que distinguen mayúsculas de minúsculas.
* Se ha agregado compatibilidad para la conversión de instrucciones de combinación no ANSI de Sybase ASE a instrucciones de combinación ANSI de SQL Server se ha ampliado a las instrucciones DELETE y UPDATE.
* Se proporcionaron opciones de conectividad adicionales para conectarse a los servidores Deybase ASE mediante el proveedor ODBC de Sybase ASE y los proveedores de ADO.NET de Sybase ASE.
* Se ha quitado la `SysDB`dependencia de una base de datos independiente denominada , que contiene las funciones de emulación de Sybase (instaladas como parte de Extension Pack).
* Se ha añadido la capacidad de instalar SSMA para Sybase Extension Pack en [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)] clústeres.
* Se ha añadido compatibilidad con versiones anteriores de proyectos creados por versiones anteriores de SSMA (v4.0 y v4.2).
* Se ha añadido la capacidad de instalar el SSMA para Sybase v5.0 producto en paralelo (SxS) con versiones anteriores de SSMA (v4.0 y v4.2).

## <a name="july-2010"></a>Julio de 2010

La versión de julio de 2010 de SSMA para Sybase agregó:

* Compatibilidad con la migración a SQL Server 2008 R2.
* Una nueva aplicación de consola SSMA para la ejecución de la línea de comandos.
* Compatibilidad con la migración de datos mediante motores de migración de datos del lado del servidor y del lado cliente.
* Compatibilidad con la instrucción "Custom SELECT" en la migración de datos.
* Compatibilidad con la migración de Sybase ASE 15.0.3 y 15.5.

## <a name="june-2008"></a>Junio de 2008

La versión de junio de 2008 de SSMA para Sybase contiene los siguientes cambios:

* Agregado SSMA Probador, que prueba automáticamente la conversión de objetos de base de datos y la migración de datos realizada por SSMA. Una vez finalizados todos los pasos de migración de SSMA, use el Probador SSMA para comprobar que los objetos convertidos funcionan de la misma manera y que todos los datos se transfirieron correctamente.
* Se ha añadido la conversión pre-SQL. El usuario ahora puede especificar declaraciones de tabla temporal (y otros objetos) para cada procedimiento de origen que se usará en la conversión.
* Mejoras añadidas en la conversión de objetos:
  * Se ha revisado la conversión.
  * Agregados y no agregados sin cláusulas de tener/grupo.
  * La `IDENTITY` función `SELECT INTO` con una instrucción.
  * Restricciones e índices agrupados en solo datos bloqueados.
  * Tablas temporales creadas por `SELECT INTO`.
  * Restricciones / índices para tablas temporales.
  * Se [!INCLUDE [ssSQL10](../../includes/sssql10-md.md)] admiten nuevos tipos de fecha y hora.
  * Compatibilidad con la conectividad y los tipos de datos de Sybase 15.0.

## <a name="may-2007"></a>Mayo de 2007

La versión de mayo de 2007 de SSMA para Sybase agregó:

* La capacidad de cargar contenido de base de datos más rápido al guardar un proyecto.
* Compatibilidad con comentarios introducidos por el usuario en el modo SQL con formato de SQL ServerSQL Server .
* Mejoras en la conversión de objetos.

## <a name="november-2006"></a>Noviembre de 2006

La versión de noviembre de 2006 de SSMA para Sybase contiene los siguientes cambios:

* Se han añadido nuevos ajustes globales:
  * Puede optar por mostrar números de línea en las ventanas del editor.
  * Puede configurar SSMA para solicitar que reemplace los objetos duplicados, o siempre o nunca reemplazar objetos duplicados durante la conversión de esquema.
* Se ha añadido una nueva opción de conversión que le permite configurar cómo SSMA controla las situaciones siguientes:
  * A `CAST` `CONVERT` o instrucción que contiene una cadena binaria.
  * Comprueba si hay valores nulos en expresiones de igualdad.
  * Tablas de proxy.
  * Números de `RAISERROR`error de mensaje de usuario para .
  * `UPDATE`instrucciones que contienen identificadores no resueltos.
* Se ha agregado una nueva opción de migración que le [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)] permite especificar cómo SSMA debe controlar las fechas que están fuera del intervalo de fechas.
* Se ha añadido una configuración **de SQL con formato** en la pestaña **SQL,** que da formato al código para mejorar la legibilidad.
* Corrección de errores, incluyendo:
  * SSMA ahora `LOCK TABLE <table> IN { SHARED | EXCLUSIVE } MODE` convierte instrucciones agregando una `TABLOCK` o `TABLOCKX` sugerencia a la consulta posterior `SELECT` en la tabla.
  * Ahora se agregan las conversiones necesarias cuando se utilizan tipos binarios en expresiones de caracteres.
  * Mejoras en la memoria y el rendimiento.

## <a name="july-2006"></a>Julio de 2006

La versión de julio de 2006 de SSMA para Sybase fue la versión inicial.

## <a name="see-also"></a>Vea también

[Introducción a SSMA para Sybase &#40;SybaseToSQL&#41;](../../ssma/sybase/getting-started-with-ssma-for-sybase-sybasetosql.md)
