---
title: Novedades de SSMA para DB2 (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 12/04/2019
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 1cc38f85-3caa-42d0-8c76-a380c1d15c67
author: HJToland3
ms.author: Shamikg
ms.openlocfilehash: 75fbcbef02dc19dac47d96431118b75df262b685
ms.sourcegitcommit: 26868c8ac3217176b370d972a26d307598a10328
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/05/2019
ms.locfileid: "74834302"
---
# <a name="whats-new-in-ssma-for-db2-db2tosql"></a>Novedades de SSMA para DB2 (DB2ToSQL)

En este artículo se enumeran los cambios de SQL Server Migration Assistant (SSMA) para DB2 en cada versión.

## <a name="ssma-v85"></a>SSMA v 8.5

La versión v 8.5 de SSMA para DB2 se ha mejorado con compatibilidad para la autenticación Azure Active Directory y la compatibilidad básica con características JSON en SQL Server, junto con un conjunto de correcciones diseñado para mejorar la facilidad de uso y el rendimiento.

Además, SSMA para DB2 se ha mejorado con:

* Compatibilidad para agregar la conversión para la instrucción GET Diagnostics con ROW_NUMBER.
* Corrección de un error relacionado con espacios al principio del nombre del objeto que no se respeta.

> [!IMPORTANT]
> Con SSMA v 8.5, .net 4.7.2 es un requisito previo de instalación. Si necesita instalar esta versión, puede descargar el archivo en tiempo de ejecución desde [aquí](https://dotnet.microsoft.com/download/dotnet-framework/net472).

## <a name="ssma-v84"></a>SSMA v 8.4

La versión v 8.4 de SSMA para DB2 se ha mejorado con correcciones de destino diseñadas para solucionar problemas de accesibilidad y corregir un error relacionado con las columnas de índice máximo (para permitir 32 en lugar de 16) para SQL Server 2016 y versiones posteriores.

> [!IMPORTANT]
> Con las versiones de SSMA 7,4 a 8,4, .net 4.5.2 es un requisito previo de instalación.

## <a name="ssma-v83"></a>SSMA v 8.3

La publicación v 8.3 de SSMA para DB2 se ha mejorado con correcciones de destino diseñadas para mejorar la calidad y las métricas de conversión. Además, esta versión de SSMA para DB2 proporciona correcciones que:

* Solucionar problemas de accesibilidad
* Agregar compatibilidad básica para el tipo ' hierarchyid ' en SQL Server
* Reemplazar el uso de la función TRIM en consultas de detección de z/OS con RTRIM/LTRIM
* Permitir al usuario especificar la colección de paquetes al conectarse en "modo estándar" (el valor predeterminado es NULLID)
* Agregar conversión para CREATE TABLE como SELECT
* Mejorar las conversiones de las tablas temporales globales
* Solucionar un problema con la comprobación de la unicidad de objetos para dar prioridad a las tablas a través de las restricciones, si los nombres entran en conflicto
* Solucionar un problema con la carga de valores de columna predeterminados para la fecha y la marca de tiempo para z/OS
* Compatibilidad con el carácter de salto de línea Unicode (también conocido como carácter)
* Solucionar un problema con la conversión de cursor con la cláusula Return TO que falta
* Agregar compatibilidad para etiquetas e ir

## <a name="ssma-v82"></a>SSMA v 8.2

La versión v 8.2 de SSMA para DB2 se ha mejorado con para solucionar problemas con conexiones a Azure SQL Database desde la herramienta de consola SSMA y que faltan COUNT_BIG columna en la declaración de vistas durante la conversión. Además, esta versión incluye un conjunto de correcciones de destino diseñado para mejorar la calidad y las métricas de conversión, así como las correcciones para:

* Un problema con los índices no clúster deshabilitados después de la migración de datos.
* Detección de .NET Framework durante la instalación silenciosa.
* Un bloqueo intermitente que se produce cuando se descarga una nueva versión.

> [!NOTE]
> Un problema conocido con la actualización automática puede producir un error en una actualización de SSMA v 8.1 a v 8.2. Si se produce este error, descargue la nueva versión e instálela manualmente.

## <a name="ssma-v81"></a>SSMA v 8.1

La versión v 8.1 de SSMA para DB2 se ha mejorado para proporcionar correcciones dirigidas diseñadas para mejorar la calidad y las métricas de conversión.

> [!NOTE]
> Un problema conocido con la actualización automática puede producir un error en una actualización de SSMA v 8.0 a v 8.1. Si se produce este error, descargue la nueva versión e instálela manualmente.

## <a name="ssma-v80"></a>SSMA v 8.0

La versión 8.0 de SSMA para DB2 se ha mejorado para proporcionar soluciones de destino diseñadas para mejorar la calidad y las métricas de conversión. Esta versión también ofrece las siguientes características nuevas:

* Compatibilidad con **instancia administrada de Azure SQL Database** como destino. Ahora puede crear nuevos proyectos que tengan como destino Instancia administrada de Azure SQL Database:

  ![Proyecto de MI de base de SQL](../media/ssma-newproject-sqldbmi.png)

* **Asesor de corrección**posterior a la conversión. Obtenga más información [aquí](https://blogs.msdn.microsoft.com/datamigration/2019/02/17/%20accelerate-your-oracle-migrations-with-new-machine-learning-capabilities-in-ssma/).

* Selección preliminar de base de datos/esquema.

  Al conectarse al origen, el usuario puede seleccionar las bases de datos o los esquemas de interés. Si selecciona solo los esquemas que va a migrar, se ahorrará tiempo durante la conexión inicial y se mejorará el rendimiento global de SSMA.

  ![SSMA (objetos de filtro)](../media/ssma-filter-objects.png)

## <a name="ssma-v710"></a>SSMA v 7.10

La versión v 7.10 de SSMA para DB2 contiene los siguientes cambios:

* Soluciones de destino diseñadas para proporcionar seguridad adicional y protección de la privacidad para satisfacer los cambios en los requisitos globales.
* Corrección para la conversión de los bloques BEGIN-END.

## <a name="ssma-v79"></a>SSMA v 7.9

La versión v 7.9 de SSMA para DB2 contiene los siguientes cambios:

* Correcciones dirigidas que mejoran las métricas de calidad y conversión.
* Compatibilidad en la línea de comandos de SSMA para modificar la asignación de tipos de datos y las preferencias del proyecto.
* Compatibilidad para la migración de datos con SQL Server Integration Services (SSIS). Después de convertir el esquema, es posible crear un paquete SSIS mediante el uso de una opción del menú contextual.
* También se ha modificado el cuadro de diálogo de conexión Azure SQL Database en SSMA para especificar el nombre completo del servidor. En versiones anteriores de SSMA, el prefijo Azure SQL Database tenía que mencionarse explícitamente dentro de la configuración de los proyectos.

## <a name="ssma-v78"></a>SSMA v 7.8

La versión v 7.8 de SSMA para DB2 contiene los siguientes cambios:

* Cambiar la asignación de tipos resaltada en la configuración del proyecto.
* La capacidad de los usuarios de deshabilitar la telemetría.

## <a name="ssma-v77"></a>SSMA v 7.7

La versión v 7.7 de SSMA para DB2 contiene los siguientes cambios:

* Correcciones dirigidas que mejoran las métricas de calidad y conversión.
* En función de la demanda popular, la versión de 32 bits de SSMA para DB2 vuelve a ser. En comparación con la implementación anterior (antes de v 7.4), hay dos paquetes de instalador, pero no se pueden instalar en paralelo. Como resultado, debe elegir la versión más adecuada en función de los componentes de conectividad que tenga. Siempre es preferible usar la versión de 64 bits, si es posible.

## <a name="ssma-v76"></a>SSMA v 7.6

La versión v 7.6 de SSMA para DB2 se ha mejorado con correcciones de destino que mejoran las métricas de calidad y conversión y admiten SQL Server 2017 (versión preliminar pública). La compatibilidad con SQL Server 2017 en Windows y Linux está en versión preliminar pública y no debe usarse para migraciones de producción.

## <a name="ssma-v75"></a>SSMA v 7.5

La versión v 7.5 de SSMA para DB2 se ha mejorado con varias mejoras para garantizar una mayor accesibilidad para las personas con discapacidades.

## <a name="ssma-v74"></a>SSMA v 7.4

La versión v 7.4 de SSMA para DB2 contiene los siguientes cambios:

* La opción **tiempo de espera de consulta** ahora está disponible durante la detección de objetos de esquema en el origen y el destino.

  ![opción de tiempo de espera de consulta](../media/query-timeout_red.png)

* La métrica de calidad y conversión se ha mejorado con las correcciones de destino, en función de los comentarios de los clientes.

  > [!IMPORTANT]
  > .Net 4.5.2 es un requisito previo para instalar SSMA v 7.4. Además, a partir de v 7.4, se ha interrumpido la versión de 32 bits de SSMA.

## <a name="ssma-v73"></a>SSMA v 7.3

La versión v 7.3 de SSMA para DB2 contiene los siguientes cambios:

* Métrica de calidad y conversión mejorada con correcciones de destino basadas en los comentarios de los clientes.
* El marco de extensibilidad de SSMA expuesto a través de los siguientes elementos:
  * Exportar funcionalidad a un proyecto SQL Server Data Tools (SSDT).
    * Ahora puede exportar scripts de esquema de SSMA a un proyecto de SSDT. Puede usar los scripts de esquema para realizar cambios de esquema adicionales e implementar la base de datos.

      ![Comando Guardar como proyecto de SSDT](../media/export-schema-scripts_red.png)
  * Bibliotecas que puede usar SSMA para realizar conversiones personalizadas.
    * Ahora puede construir código que pueda controlar las conversiones de sintaxis personalizadas y las conversiones que no se administraron previamente mediante SSMA.
      * En esta entrada de blog se ofrecen instrucciones sobre cómo construir un convertidor personalizado, que [amplían las capacidades de conversión de SQL Server Migration Assistant](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/).
      * Descargue un proyecto de ejemplo para la conversión de esta [entrada de blog](https://blogs.msdn.microsoft.com/datamigration/ssmafororacleconversionsample/).

## <a name="ssma-v72"></a>SSMA v 7.2

La versión v 7.2 de SSMA para DB2 contiene los siguientes cambios:

* Métrica de calidad y conversión mejorada con correcciones de destino basadas en los comentarios de los clientes.
* Mejoras en la telemetría para proporcionar mejores puntos de datos para solucionar problemas de los clientes y mejorar las tasas de conversión de SSMA.

## <a name="ssma-v71"></a>SSMA v 7.1

La versión v 7.1 de SSMA para DB2 contiene los siguientes cambios:

* SQL Server 2017 en Windows y Linux CTP1 es ahora una plataforma de destino admitida para la migración. Esta característica se encuentra en Technical Preview y permite el movimiento de datos y esquemas a los servidores SQL Server de destino.
* Compatibilidad con las actualizaciones automáticas para descargar la versión más reciente de SSMA en cuanto esté disponible.
* Los binarios instalables de SSMA se entregan ahora a través de los archivos de paquete de Windows Installer (. msi).

## <a name="may-2016"></a>Mayo de 2016

La versión de mayo de 2016 de SSMA para DB2 contiene los siguientes cambios:  

* Compatibilidad agregada para SQL Server 2016.
* Se ha agregado la conversión de tablas en memoria y normales de DB2 para SQL Server características en memoria y hekaton.
* Conversión agregada de controles de acceso de DB2 a objetos de directiva de SQL Server (Seguridad de nivel de fila para DB2).
* Se ha agregado la conversión de tablas con versiones del sistema DB2 en SQL Server tablas temporales.
* Analizador y resolución de DB2 mejorados.
* Se quitó la comprobación del instalador para .net 2,0.
* Se quitó un archivo *. dll innecesario del instalador de DB2.
* Se han corregido los comandos "guardar proyecto" y "Abrir proyecto" para la consola de SSMA.
* Se corrigió el comando "securepassword" para la consola de SSMA.
* Recuento fijo de objetos para la carga inicial.
* Se corrigió el error en la configuración global.
  
## <a name="march-2016"></a>marzo de 2016

La versión de vista previa de marzo de 2016 de SSMA para DB2 agrega compatibilidad para la migración a SQL Server 2016.

## <a name="january-2016"></a>Enero de 2016

La versión de mantenimiento de enero de 2016 de SSMA para DB2 contiene los siguientes cambios:  
  
* Se ha agregado compatibilidad con varias funciones estándar.  
* Errores corregidos del analizador de DB2.  
* Se corrigió la compatibilidad con zOS de DB2 V9 (RFC 5690920).  
* Se corrigieron errores de identificador sin resolver de DB2 durante la conversión.  
* Se ha agregado el elemento de menú Ver registro a SSMA (RFC 5706203).  
* Telemetría agregada.
  
## <a name="november-2014"></a>Noviembre de 2014

La versión de noviembre de 2014 de SSMA para DB2 fue la versión inicial.
