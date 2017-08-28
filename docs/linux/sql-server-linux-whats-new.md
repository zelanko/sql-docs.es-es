---
title: "' S New para SQL Server de 2017 RC1 en Linux | Documentos de Microsoft"
description: "Este tema destacan cuáles son las novedades de la versión actual de SQL Server 2017 en Linux."
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 08/02/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 456b6f31-6b97-4e31-80ab-b40151ec4868
ms.translationtype: MT
ms.sourcegitcommit: ea75391663eb4d509c10fb785fcf321558ff0b6e
ms.openlocfilehash: 649c7cbd03b6d2e61dbbb572a34cdbcd2a7ab7cd
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="whats-new-for-sql-server-2017-on-linux"></a>Novedades de SQL Server 2017 en Linux

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

Este tema describe lo que es una novedad de SQL Server 2017 ejecutando en Linux.

## <a name="rc2"></a>RC2

La versión de RC2 contiene varias correcciones de errores y mejoras.

## <a name="rc1"></a>RC1

La versión RC1 contiene las siguientes mejoras y correcciones:

- Habilitar capa transparente (TLS) para las conexiones cifradas. Para obtener más información, consulte [cifrar conexiones a SQL Server en Linux](sql-server-linux-encrypted-connections.md).
- Habilitado [autenticación de Active Directory](sql-server-linux-active-directory-authentication.md).
- Habilitado [correo electrónico de base de datos](../relational-databases/database-mail/database-mail.md).
- Se agregó compatibilidad de IPV6.
- Variables de entorno agregada para la instalación inicial de SQL Server. Para obtener más información, consulte [configuración configurar SQL Server con las variables de entorno en Linux](sql-server-linux-configure-environment-variables.md).
- Quitar **sqlpackage** de instalar los archivos binarios. SqlPackage puede seguir ejecutando en Linux remotamente desde Windows.
- Compartir conjuntos del recurso Agente de discos clúster que el nombre del recurso como lo hace en una instancia de clúster de conmutación por error de SQL Server de Windows. `@@ServerName`Devuelve el nombre de recursos de clúster de disco compartido de SQL Server; antes de RC1, devuelve el nombre del nodo del clúster al que pertenece el recurso.

## <a name="ctp-21"></a>CTP 2.1

La versión de CTP 2.1 contiene las siguientes mejoras y correcciones:

- Agregar [variables de entorno para configurar el servicio de SQL Server](sql-server-linux-configure-environment-variables.md).
- [MSSQL-conf](sql-server-linux-configure-mssql-conf.md) requiere ahora la convención de nomenclatura de dos partes para la configuración.
- El [scripter mssql](https://github.com/Microsoft/sql-xplat-cli) herramienta. Esta utilidad permite a los desarrolladores, administradores y administradores del sistema generar `CREATE` y `INSERT` scripts de Transact-SQL de objetos de base de datos en las bases de datos de SQL Server, base de datos de SQL Azure y almacenamiento de datos de SQL Azure desde la línea de comandos.
- El [herramienta DBFS](https://github.com/Microsoft/dbfs). Se trata de una herramienta de código abierto que permite que los DBA y administradores del sistema supervisar SQL Server más fácilmente mediante la exposición de datos en directo de vistas de administración dinámica (DMV) de SQL Server como archivos virtuales en un directorio virtual en sistemas operativos Linux.
- SQL Server Integration Services (SSIS) se ejecuta ahora en Linux. Además, hay un nuevo paquete que le permite ejecutar paquetes SSIS en Linux desde la línea de comandos. Para obtener más información, consulte el [blog post anunciar la compatibilidad con SSIS para Linux](https://blogs.msdn.microsoft.com/ssis/2017/05/17/ssis-helsinki-is-available-in-sql-server-vnext-ctp2-1/). Con SSIS en Linux CTP 2.1 actualizar, los paquetes SSIS pueden usar conexiones de ODBC en Linux. Para obtener más información, consulte el [entrada del blog del anuncio de compatibilidad con ODBC en Linux](https://blogs.msdn.microsoft.com/ssis/2017/06/16/odbc-is-supported-in-ssis-on-linux-ssis-helsinki-ctp2-1-refresh/).

## <a name="ctp-20"></a>EN CTP 2.0

La versión de CTP 2.0 contiene las siguientes mejoras y correcciones:

- Agregar **trasvase de registros** funcionalidad de agente SQL Server.
- Mensajes en otros idiomas de mssql-conf.
- Formato de ruta de acceso de Linux ahora son compatibles en el motor de SQL Server. Pero es compatible con para "C:\\" las rutas de acceso con prefijo continuará.
- Habilitado DMV **sys.dm_os_file_exists**.
- Habilitado DMV **sys.fn_trace_gettable**.
- Agregar [modo de seguridad estricta de CLR](/sql/database-engine/configure-windows/clr-strict-security).
- Gráfico SQL.
- Regeneraciones de índice en línea reanudables.
- Procesamiento de consultas adaptable.
- Ha agregado codificación UTF-8 para los archivos de sistema, incluidos los archivos de registro.
- Se ha corregido bases de datos en memoria limitación de ubicación. 
- Agregar nuevo tipo de clúster `CLUSTER_TYPE = EXTERNAL` para configurar un grupo de disponibilidad para lograr alta disponibilidad.
- Corrija el agente de escucha del grupo de disponibilidad para el enrutamiento de solo lectura.
- Soporte técnico de producción para los clientes del programa de adopción temprana (EAP). Suscríbase [aquí](http://aka.ms/eapsignup).

## <a name="ctp-14"></a>CTP 1.4

La versión 1.4 de CTP contiene las siguientes mejoras y correcciones:

- Habilita la [Agente SQL Server](sql-server-linux-setup-sql-agent.md).
  - Habilitar la funcionalidad de trabajos de T-SQL.
- Errores de zona horaria fijo:
  - Compatibilidad con la zona horaria Asia o Kolkhata.
  - Función GETDATE() fija.
- Red Async I / 0 mejoras:
  - Mejoras importantes de rendimiento de la carga de trabajo de OLTP en memoria.
- Imagen de docker ahora incluye utilidades de línea de comandos de SQL Server. (sqlcmd y bcp).
- Habilitar compatibilidad de interfaz de dispositivo Virtual (VDI) para las copias de seguridad.
- Ubicación de TempDB ahora puede modificarse después de la instalación con `ALTER DATABASE`.

## <a name="ctp-13"></a>CTP 1.3

La versión 1.3 de CTP contiene las siguientes mejoras y correcciones:

- Habilitado [búsqueda de texto completo](sql-server-linux-setup-full-text-search.md) característica.
- Habilitar Always On [funcionalidad de grupos de disponibilidad](sql-server-linux-availability-group-overview.md) para lograr alta disponibilidad.
- Funcionalidad adicional de **mssql-conf**:
  - Primera instalación de tiempo mediante **mssql-conf**. Consulte el uso de mssql-conf en el [guías de instalación](sql-server-linux-setup.md#platforms).
  - Habilitar los grupos de disponibilidad. Consulte la [tema de los grupos de disponibilidad](sql-server-linux-availability-group-overview.md).
- Ruta de acceso de Linux nativo fija la compatibilidad para grupos de archivos OLTP en memoria.
- Habilitar la funcionalidad de dm_os_host_info DMV.

## <a name="ctp-12"></a>CTP 1.2

La versión 1.2 de CTP contiene las siguientes mejoras y correcciones:

- Compatibilidad con [SUSE Linux Enterprise Server v12 SP2](quickstart-install-connect-suse.md).
- Correcciones de errores principales mejoras del motor y la estabilidad.
- Imagen de docker: 
  - Fijo [emitir #1](https://github.com/Microsoft/mssql-docker/issues/1) mediante la adición de Python para la imagen.
  - Quitar `/opt/mssql/data` como el volumen de manera predeterminada.
- Actualiza a .NET 4.6.2.

## <a name="ctp-11"></a>CTP 1.1

La versión de CTP 1.1 contiene las siguientes mejoras y correcciones:

- Compatibilidad con Red Hat Enterprise Linux versión 7.3.
- Compatibilidad con Ubuntu 16,10.
- Capa de Docker SO actualizado para Ubuntu 16.04.
- Se corrigieron problemas de telemetría en imagen de Docker.
- Secuencia de comandos de instalación de SQL Server fijo relacionados con errores.
- Mejora el rendimiento de módulos compilados de forma nativa de T-SQL, incluidos:
  - **OPENJSON**, **FOR JSON**, **JSON** elementos integrados.
  - Columnas calculadas (solo se permiten índices en columnas calculadas persistentes, pero no en las columnas calculadas no persistentes para tablas en memoria).
  - **CROSS APPLY** operaciones.
- Nuevas características del lenguaje:
  - Funciones de cadena: **recortar**, **CONCAT_WS**, **TRANSLATE** y **STRING_AGG** con compatibilidad para **WITHIN GROUP (ORDER BY)**.
  - **La importación masiva** ahora es compatible con formato CSV y el almacenamiento de blobs de Azure como origen de archivo.

En el modo de compatibilidad 140:

- Mejora el rendimiento de las actualizaciones de índices de almacén de columnas no agrupado en el caso cuando la fila se encuentra en el almacén delta. Cambió de eliminación e inserción de operaciones para actualizar. Cambiar también las formas de plan de todo para restringir.
- Las consultas en modo por lotes admiten ahora "bucles de comentarios de concesiones de memoria". Esto mejorará la simultaneidad y el rendimiento en sistemas que ejecutan consultas repetidas que utilizan el modo por lotes. Esto puede permitir que se ejecuten en sistemas que están bloqueando de otro modo en memoria antes de iniciar las consultas más consultas.
- Mejorar el rendimiento en el paralelismo de modo por lotes sin tener en cuenta planes triviales para planes de modo por lotes permitir a los planes paralelos que pueden seleccionar en su lugar en columnstores. 

[Mejoras del Service Pack 1](https://blogs.msdn.microsoft.com/sqlreleaseservices/sql-server-2016-service-pack-1-sp1-released/) en esta versión CTP1.1:
- Clonación de CLR, Filestream o Filetable, los objetos en memoria y almacén de consultas de base de datos.
- **CREAR** o **ALTER** operadores para los objetos de programación.
- Nueva **sugerencia USE** opción para proporcionar sugerencias para el procesador de consultas de consulta. Obtenga más información aquí: [sugerencias de consulta](https://msdn.microsoft.com/en-us/library/ms181714.aspx).
- Cuenta de servicio SQL ahora puede identificar mediante programación habilitar Bloquear páginas en memoria y la inicialización instantánea de archivos de permisos.
- Compatibilidad con el número de archivos de TempDB, tamaño de archivo y configuración de crecimiento de archivo.
- Diagnóstico extendido en el plan de presentación XML.
- Por cada operador ligera consulta ejecución de generación de perfiles.
- Nueva función de administración dinámica **sys.dm_exec_query_statistics_xml**.
- Nueva función de administración dinámica para las estadísticas incrementales.
- Quitado en memoria con ruido relacionados con mensajes de registro de registro de errores.
- Diagnóstico de latencia de AlwaysOn mejorado.
- Limpiar el seguimiento de cambios Manual.
- **DROP TABLE** admite para la replicación.
- **BULK INSERT** en montones con **automática TABLOCK** en TF 715.
- Paralelo **INSERT... Seleccione** cambios para tablas temporales locales.

Obtener más información sobre estas correcciones en el [descripción de la versión de Service Pack 1](https://blogs.msdn.microsoft.com/sqlreleaseservices/sql-server-2016-service-pack-1-sp1-released/).

Muchas mejoras del motor de base de datos se aplican a Windows y Linux. La única excepción sería de características del motor de base de datos que no se admiten en Linux. Para obtener más información, consulte [What's New en SQL Server 2017 (motor de base de datos)](https://msdn.microsoft.com/library/mt775028).

## <a name="see-also"></a>Vea también

Para los requisitos de instalación, áreas de características no compatibles y problemas conocidos, consulte [notas de la versión de SQL Server 2017 en Linux](sql-server-linux-release-notes.md).

