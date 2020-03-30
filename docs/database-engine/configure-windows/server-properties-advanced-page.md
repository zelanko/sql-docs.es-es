---
title: Propiedades del servidor (página Opciones avanzadas) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql13.swb.serverproperties.advanced.f1
ms.assetid: cc5e65c2-448e-4f37-9ad4-2dfb1cc84ebe
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 1672b245f061f521c9114bca71f723fe75553c96
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2020
ms.locfileid: "68025591"
---
# <a name="server-properties---advanced-page"></a>Propiedades del servidor (página Opciones avanzadas)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Utilice esta página para ver o modificar la configuración avanzada del servidor.  
  
 **Para ver las páginas Propiedades del servidor**  
  
-   [Ver o cambiar las propiedades del servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/view-or-change-server-properties-sql-server.md)  
  
## <a name="containment"></a>Containment  
 Habilitar bases de datos independientes  
 Indica si esta instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permite bases de datos independientes. Cuando es **True**, una base de datos independiente puede crearse, restaurarse o conectarse. Cuando es **False**, una base de datos independiente no puede crearse, restaurarse ni conectarse a esta instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Cambiar la propiedad de independencia puede afectar a la seguridad de la base de datos. Habilitar las bases de datos independientes permite a los propietarios de bases de datos conceder acceso a este [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Si se deshabilitan las bases de datos independientes, se puede impedir que los usuarios se conecten. Para conocer el impacto en la propiedad de independencia, vea [Contained Databases](../../relational-databases/databases/contained-databases.md) y [Security Best Practices with Contained Databases](../../relational-databases/databases/security-best-practices-with-contained-databases.md).  
  
## <a name="filestream"></a>FILESTREAM  
 **Nivel de acceso de FILESTREAM**  
 Muestra el nivel actual de compatibilidad con FILESTREAM en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para cambiar el nivel de acceso, seleccione uno de los valores siguientes:  
  
 **Deshabilitada**  
 Los datos de objeto binario grande (BLOB) no pueden almacenarse en el sistema de archivos. Este es el valor predeterminado.  
  
 **Acceso Transact-SQL habilitado**  
 Los datos FILESTREAM son accesibles mediante [!INCLUDE[tsql](../../includes/tsql-md.md)], pero no a través del sistema de archivos.  
  
 **Acceso total habilitado**  
 Los datos FILESTREAM son accesibles mediante [!INCLUDE[tsql](../../includes/tsql-md.md)] y a través del sistema de archivos.  
  
 Al habilitar FILESTREAM por primera vez, puede que tenga que reiniciar el equipo para configurar los controladores.  
  
 **Nombre del recurso compartido de FILESTREAM**  
 Muestra el nombre de solo lectura del recurso compartido FILESTREAM que se seleccionó durante la instalación. Para obtener más información, vea [FILESTREAM &#40;SQL Server&#41;](../../relational-databases/blob/filestream-sql-server.md).  
  
## <a name="miscellaneous"></a>Varios  
 **Permitir que los desencadenadores activen otros**  
 Permite que los desencadenadores activen otros desencadenadores. Los desencadenadores pueden anidarse hasta un máximo de 32 niveles. Para obtener más información, vea la sección "Desencadenadores anidados" en [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md).  
  
 **Umbral de procesos bloqueados**  
 El umbral, en segundos, en el que se generan los informes de procesos bloqueados. El umbral puede establecerse en un valor comprendido entre 0 y 86.400. De manera predeterminada, se producen informes de procesos no bloqueados. Para obtener más información, vea [blocked process threshold (opción de configuración del servidor)](../../database-engine/configure-windows/blocked-process-threshold-server-configuration-option.md).  
  
 **Umbral de cursor**  
 Especifica el número de filas del conjunto de cursores en el que se generan de manera asincrónica los conjuntos de claves del cursor. Cuando los cursores generan un conjunto de claves para un conjunto de resultados, el optimizador de consultas calcula el número de filas que se va a devolver para ese conjunto de resultados. Si el optimizador de consultas calcula que el número de filas devuelto es superior a este umbral, el cursor se genera de manera asincrónica, lo que permite al usuario capturar las filas del cursor mientras sigue llenándose. De lo contrario, el cursor se genera de manera sincrónica y la consulta espera a que se devuelvan todas las filas.  
  
 Si se establece en el valor -1, todos los conjuntos de claves se generan de manera sincrónica; esto beneficia a los conjuntos de cursores pequeños. Si se establece en el valor 0, todos los conjuntos de claves del cursor se generan de manera asincrónica. Con otros valores, el optimizador de consultas compara el número de filas esperadas del conjunto de cursores y genera asincrónicamente el conjunto de claves si éste supera el número establecido. Para más información, consulte [Establecer la opción de configuración del servidor Umbral de cursor](../../database-engine/configure-windows/configure-the-cursor-threshold-server-configuration-option.md).  
  
 **Idioma de texto completo predeterminado**  
 Especifica un idioma predeterminado para las columnas indizadas de texto completo. El análisis lingüístico de los datos de texto completo indizados depende del idioma de los datos. El valor predeterminado de esta opción es el idioma del servidor. Para saber qué idioma corresponde al valor mostrado, vea [sys.fulltext_languages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql.md).  
  
 **Idioma predeterminado**  
 Especifica el idioma predeterminado para todos los nuevos inicios de sesión, a menos que se especifique otro.  
  
 **Opción de actualización de catálogo de texto completo**  
 Controla cómo se migran los índices de texto completo cuando se actualiza una base de datos de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Esta propiedad se aplica a la actualización al adjuntar una base de datos, restaurar una copia de seguridad de base de datos, restaurar una copia de seguridad de archivo o copiar la base de datos mediante el Asistente para copiar bases de datos.  
  
 Las alternativas son las siguientes:  
  
 **Importar**  
 Se importan los catálogos de texto completo. Esta operación es significativamente más rápida que **Volver a generar**. Sin embargo, un catálogo de texto completo importado no utiliza los divisores de palabras nuevos y mejorados que se incluyeron en [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]. Por consiguiente, podría querer volver a generar los catálogos de texto completo finalmente.  
  
 Si un catálogo de texto completo no está disponible, se vuelven a generar los índices de texto completo asociados. Esta opción solo está disponible para bases de datos de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] .  
  
 **Recompilación**  
 Los catálogos de texto completo se vuelven a generar con los separadores de palabras nuevos y mejorados. La regeneración de los índices puede llevar cierto tiempo y, después de la actualización, podría ser necesaria una cantidad significativa de CPU y de memoria.  
  
 **Reset**  
 Los catálogos de texto completo se restablecen. [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Los archivos de catálogo de texto completo se quitan, pero los metadatos de los catálogos de texto completo y los índices de texto completo se conservan. Después de actualizarse, todos los índices de texto completo quedan deshabilitados para el seguimiento de cambios y los rastreos no se inician de forma automática. El catálogo permanecerá vacío hasta que se emita manualmente un rellenado completo después de que se complete la actualización.  
  
 Para obtener más información sobre cómo elegir la opción de actualización de texto completo, vea [Actualizar la búsqueda de texto completo](../../relational-databases/search/upgrade-full-text-search.md).  
  
> [!NOTE]  
>  La opción de actualización de texto completo también se puede establecer con la acción [sp_fulltext_service](../../relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql.md)upgrade_option.  
  
 Después de adjuntar, restaurar o copiar una base de datos de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], queda disponible inmediatamente y se actualiza a continuación de forma automática. Si la base de datos tiene índices de texto completo, el proceso de actualización los importa, los restablece o los vuelve a generar, en función del valor de la propiedad del servidor **Opción de actualización de texto completo** . Si la opción de actualización se establece en **Importar** o en **Volver a generar**, los índices de texto completo no estarán disponibles durante la actualización. Dependiendo de la cantidad de datos que se indicen, la importación puede requerir varias horas y volver a generar puede requerir hasta diez veces más. Tenga en cuenta también que si la opción de actualización se establece en **Importar**y no hay disponible ningún catálogo de texto completo, se vuelven a generar los índices de texto completo asociados. Para obtener más información sobre cómo ver o cambiar la configuración de la propiedad **Opción de actualización de texto completo** , vea [Administrar y supervisar la búsqueda de texto completo para una instancia de servidor](../../relational-databases/search/manage-and-monitor-full-text-search-for-a-server-instance.md).  
  
 **Tamaño de replicación de texto máximo**  
 Especifica el tamaño máximo (en bytes) de los datos de tipo **text**, **ntext**, **varchar(max)** , **nvarchar(max)** , **xml**e **image** que se pueden agregar a una columna replicada o capturada en una sola instrucción INSERT, UPDATE, WRITETEXT o UPDATETEXT. El cambio realizado en este valor surte efecto de forma inmediata. Para más información, consulte [Establecer la opción de configuración del servidor Tamaño de replicación de texto máximo](../../database-engine/configure-windows/configure-the-max-text-repl-size-server-configuration-option.md).  
  
 **Buscar procedimientos de inicio**  
 Especifica que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] recorrerá al iniciarse la ejecución automática de los procedimientos almacenados. Si se establece en **True**, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] recorre y ejecuta todos los procedimientos almacenados que se ejecutan automáticamente definidos en el servidor. Si se establece en **False** (valor predeterminado), no se recorre ningún procedimiento. Para más información, consulte [Establecer la opción de configuración del servidor Buscar procedimientos de inicio](../../database-engine/configure-windows/configure-the-scan-for-startup-procs-server-configuration-option.md).  
  
 **Fecha límite de año de dos dígitos**  
 Indica el número de año más alto que se puede escribir como un año de dos dígitos. El año que se muestra y los 99 anteriores se pueden escribir con formato de dos dígitos. Todos los demás años se deben escribir con formato de cuatro dígitos.  
  
 Por ejemplo, el valor predeterminado 2049 indica que la fecha escrita como "14/3/49" se interpretará como 14 de marzo de 2049 y la fecha escrita como "14/3/50", como 14 de marzo de 1950. Para más información, consulte [Establecer la opción de configuración del servidor Fecha límite de año de dos dígitos](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md).  
  
## <a name="network"></a>Red  
 **Tamaño de paquete de red**  
 Establece el tamaño de paquete (en bytes) que se utiliza en toda la red. El valor predeterminado es 4.096 bytes. Si una aplicación realiza operaciones de copia masiva, o bien envía o recibe una gran cantidad de datos de tipo **text** o **image** , el uso de paquetes de un tamaño superior al predeterminado puede mejorar la eficacia, ya que tiene como resultado un número menor de operaciones de lectura y escritura en la red. Si una aplicación envía y recibe pequeñas cantidades de información, puede establecer un tamaño de 512 bytes para cada paquete, lo que es suficiente para la mayor parte de las transferencias de datos. Para más información, consulte [Establecer la opción de configuración del servidor Tamaño de paquete de red](../../database-engine/configure-windows/configure-the-network-packet-size-server-configuration-option.md).  
  
> [!NOTE]  
>  No cambie el tamaño de los paquetes a menos que esté seguro de que mejorará el rendimiento. En la mayoría de las aplicaciones, el tamaño más conveniente de los paquetes es el tamaño predeterminado.  
  
 **Tiempo de espera de inicio de sesión remoto**  
 Especifica el número de segundos que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe esperar antes de volver de un intento de inicio de sesión remoto con error. Este valor de configuración afecta a las conexiones a proveedores de OLE DB establecidas para realizar consultas heterogéneas. El valor predeterminado es 20 segundos. Un valor 0 permite una espera infinita. Para más información, consulte [Establecer la opción de configuración del servidor Tiempo de espera de inicio de sesión remoto](../../database-engine/configure-windows/configure-the-remote-login-timeout-server-configuration-option.md).  
  
 El cambio realizado en este valor surte efecto de forma inmediata.  
  
## <a name="parallelism"></a>Paralelismo:  
 **Umbral de costo para paralelismo**  
 Especifica el umbral por encima del que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] crea y ejecuta planes paralelos para consultas. Este costo hace referencia al tiempo transcurrido estimado en segundos que es necesario para ejecutar el plan serie en una configuración de hardware específica. Esta opción solo debe configurarse en multiprocesadores simétricos. Para más información, consulte [Establecer la opción de configuración del servidor Umbral de costo para paralelismo](../../database-engine/configure-windows/configure-the-cost-threshold-for-parallelism-server-configuration-option.md).  
  
 **Bloqueos**  
 Establece el número máximo de bloqueos disponibles, limitando de este modo la cantidad de memoria que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utiliza para ellos. El valor predeterminado es 0, lo que permite a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] asignar y cancelar la asignación de bloqueos de manera dinámica basándose en los requisitos variables del sistema.  
  
 La configuración recomendada es permitir que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilice los bloqueos de manera dinámica. Para más información, consulte [Establecer la opción de configuración del servidor Bloqueos](../../database-engine/configure-windows/configure-the-locks-server-configuration-option.md).  
  
 **Grado máximo de paralelismo**  
 Limita el número de procesadores (hasta un máximo de 64) que deben utilizarse en la ejecución de planes paralelos. El valor predeterminado, 0, usa todos los procesadores disponibles. El valor 1 suprime la generación de planes paralelos. Un número superior a 1 limita el número máximo de procesadores que se utilizan en la ejecución de una sola consulta. Si se especifica un valor superior al número de procesadores disponibles, se utilizará el número real de procesadores disponibles. Para obtener más información, vea [Establecer la opción de configuración del servidor Grado máximo de paralelismo](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md).  
  
 **Espera de consulta**  
 Especifica el tiempo en segundos (de 0 a 2.147.483.647) que espera una consulta para utilizar los recursos antes de agotarse el tiempo de espera. Si se utiliza el valor predeterminado -1, el tiempo de espera calculado será 25 veces el costo estimado de la consulta. Para más información, consulte [Establecer la opción de configuración del servidor Espera de consulta](../../database-engine/configure-windows/configure-the-query-wait-server-configuration-option.md).  
  
## <a name="see-also"></a>Consulte también  
 [Opciones de configuración de servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)  
  
  
