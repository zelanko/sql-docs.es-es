---
title: Propiedades de la base de datos (página Opciones) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.swb.databaseproperties.options.f1
ms.assetid: a3447987-5507-4630-ac35-58821b72354d
caps.latest.revision: 65
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 6747eb3df75a585236e85de6bc0103241f5b6d8f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36202103"
---
# <a name="database-properties-options-page"></a>Propiedades de la base de datos (página Opciones)
  Utilice esta página para ver o modificar opciones de la base de datos seleccionada. Para obtener más información sobre las opciones disponibles en esta página, vea [ALTER DATABASE SET Options &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options).  
  
## <a name="page-header"></a>Encabezado de página  
 **Intercalación**  
 Especifique la intercalación de la base de datos seleccionándola en la lista. Para más información, vea [Set or Change the Database Collation](../collations/set-or-change-the-database-collation.md).  
  
 **Modelo de recuperación**  
 Especifique uno de los modelos siguientes para la recuperación de la base de datos: **Completa**, **Registro masivo**o **Simple**. Para obtener más información sobre los modelos de recuperación, vea [Modelos de recuperación &#40;SQL Server&#41;](../backup-restore/recovery-models-sql-server.md).  
  
 **Nivel de compatibilidad**  
 Especifique la versión más reciente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admitida por la base de datos. Los valores posibles son  **SQL Server 2014 (120)**,  **SQL Server 2012 (110)** y **SQL Server 2008 (100)**. Cuando una base de datos de SQL Server 2005 se actualiza a SQL Server 2014, el nivel de compatibilidad para la base de datos se cambia de 90 a 100.  El nivel de compatibilidad 90 no se admite en SQL Server 2014. Para obtener más información, vea [Nivel de compatibilidad de ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level).  
  
 **Tipo de contención**  
 Especifique ninguno o parcial para indicar que se trata de una base de datos independiente. Para obtener más información acerca de las bases de datos independientes, vea [Contained Databases](contained-databases.md). La propiedad de servidor **Habilitar bases de datos independientes** debe establecerse en **TRUE** antes de configurar una base de datos como independiente.  
  
> [!IMPORTANT]  
>  La habilitación de bases de datos parcialmente independientes delega el control sobre el acceso a la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en los propietarios de la base de datos. Para más información, vea [Security Best Practices with Contained Databases](security-best-practices-with-contained-databases.md).  
  
## <a name="automatic"></a>Automático  
 **Cerrar automáticamente**  
 Especifique si la base de datos se cierra sin problemas y libera los recursos cuando sale el último usuario. Los valores posibles son `True` y `False`. Cuando es `True`, la base de datos se cierra sin problemas y se liberan sus recursos después de que el último usuario cierre la sesión.  
  
 Creación automática de estadísticas incrementales  
 Especifique si desea utilizar la opción incremental cuando se crean estadísticas por partición. Para obtener más información sobre las estadísticas incrementales, vea [CREATE STATISTICS &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-statistics-transact-sql).  
  
 **Crear estadísticas automáticamente**  
 Especifique si la base de datos crea automáticamente estadísticas de optimización que faltan. Los valores posibles son `True` y `False`. Cuando es `True`, las estadísticas que le falten a una consulta para su optimización se generan automáticamente durante la optimización. Para obtener más información, vea [CREATE STATISTICS &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-statistics-transact-sql).  
  
 **Reducir automáticamente**  
 Especifique si los archivos de base de datos se pueden reducir periódicamente. Los valores posibles son `True` y `False`. Para más información, vea [Shrink a Database](shrink-a-database.md).  
  
 **Actualizar estadísticas automáticamente**  
 Especifique si la base de datos actualiza automáticamente las estadísticas de optimización no actualizadas. Los valores posibles son `True` y `False`. Cuando es `True`, las estadísticas desusadas que precise una consulta para su optimización se generan automáticamente durante la optimización. Para obtener más información, vea [CREATE STATISTICS &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-statistics-transact-sql).  
  
 **Actualizar estadísticas automática y asincrónicamente**  
 Cuando `True`, las consultas que inician una actualización automática de estadísticas obsoletas no esperan que las estadísticas se actualicen antes de la compilación. Las consultas posteriores utilizan las estadísticas actualizadas si están disponibles.  
  
 Cuando `False`, las consultas que inician una actualización automática de las estadísticas obsoletas esperan hasta que las estadísticas actualizadas se pueden utilizar en el plan de optimización de consultas.  
  
 Establecer esta opción en `True` no tiene ningún efecto a menos que **actualizar estadísticas automáticamente** también se establece en `True`.  
  
## <a name="containment"></a>Containment  
 En las bases de datos independientes, algunos valores que se suelen configurar en el nivel de servidor se pueden configurar en el nivel de base de datos.  
  
 **LCID del idioma de texto completo predeterminado**  
 Especifica un idioma predeterminado para las columnas indizadas de texto completo. El análisis lingüístico de los datos de texto completo indizados depende del idioma de los datos. El valor predeterminado de esta opción es el idioma del servidor. Para saber qué idioma corresponde al valor mostrado, vea [sys.fulltext_languages &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql).  
  
 **Idioma predeterminado**  
 Especifica el idioma predeterminado para todos los nuevos usuarios de bases de datos independientes, a menos que se especifique otro.  
  
 **Desencadenadores anidados habilitados**  
 Permite que los desencadenadores activen otros desencadenadores. Los desencadenadores pueden anidarse hasta un máximo de 32 niveles. Para obtener más información, vea la sección "Desencadenadores anidados" en [CREATE TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-trigger-transact-sql).  
  
 **Transformar palabras irrelevantes**  
 Suprimir un mensaje de error si las palabras irrelevantes hacen que una operación booleana en una consulta de texto completo devuelva cero filas. Para más información, vea [transform noise words Server Configuration Option](../../database-engine/configure-windows/transform-noise-words-server-configuration-option.md).  
  
 **Fecha límite de año de dos dígitos**  
 Indica el número de año más alto que se puede escribir como un año de dos dígitos. El año que se muestra y los 99 anteriores se pueden escribir con formato de dos dígitos. Todos los demás años se deben escribir con formato de cuatro dígitos.  
  
 Por ejemplo, el valor predeterminado 2049 indica que la fecha escrita como "14/3/49" se interpretará como 14 de marzo de 2049 y la fecha escrita como "14/3/50", como 14 de marzo de 1950. Para más información, consulte [Establecer la opción de configuración del servidor Fecha límite de año de dos dígitos](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md).  
  
## <a name="cursor"></a>Cursor  
 **Cierre de cursor al confirmar habilitado**  
 Especifique si los cursores se cierran tras confirmar la transacción que abre el cursor. Los valores posibles son `True` y `False`. Cuando es `True`, se cierran los cursores que estuvieran abiertos al confirmar o revertir una transacción. Cuando es `False`, estos cursores se mantienen abiertos al confirmarse una transacción. Cuando es `False`, si se revierte una transacción, se cierran todos los cursores, excepto los definidos como INSENSITIVE o STATIC. Para obtener más información, vea [SET CURSOR_CLOSE_ON_COMMIT &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-cursor-close-on-commit-transact-sql).  
  
 **Cursor predeterminado**  
 Especifica el comportamiento predeterminado del cursor. Cuando es `True`, el valor predeterminado de las declaraciones de cursor es LOCAL. Cuando `False`, [!INCLUDE[tsql](../../includes/tsql-md.md)] cursores como valor predeterminado GLOBAL.  
  
## <a name="filestream"></a>FILESTREAM  
 **Nombre de directorio de FILESTREAM**  
 Especifique el nombre del directorio para los datos de FILESTREAM asociados a la base de datos seleccionada.  
  
 **Acceso sin transacciones de FILESTREAM**  
 Especifique una de las siguientes opciones para el acceso no transaccional a través del sistema de archivos a los datos de FILESTREAM almacenados en tablas FileTable: **OFF**, **READ_ONLY**o **FULL**. Si FILESTREAM no está habilitado en el servidor, este valor se establece en OFF y está deshabilitado. Para obtener más información, vea [FileTables &#40;SQL Server&#41;](../blob/filetables-sql-server.md).  
  
## <a name="miscellaneous"></a>Varios  
 **Valor ANSI NULL predeterminado**  
 Permitir valores null para todos los tipos de datos definidos por el usuario o las columnas que no se definan explícitamente como `NOT NULL` durante un `CREATE TABLE` o `ALTER TABLE` instrucción (estado predeterminado). Para obtener más información, vea [SET ANSI_NULL_DFLT_ON &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-ansi-null-dflt-on-transact-sql) y [SET ANSI_NULL_DFLT_OFF &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-ansi-null-dflt-off-transact-sql).  
  
 **Valores NULL ANSI habilitados**  
 Especifica el comportamiento de los operadores de comparación Es igual a (`=`) y No es igual a (`<>`) cuando se usan con valores NULL. Los valores posibles son `True` (activado) y `False` (desactivado). Cuando es `True`, todas las comparaciones con un valor NULL se evalúan como UNKNOWN. Cuando `False`, las comparaciones de valores no UNICODE con un valor null se evalúan como `True` si ambos valores son NULL. Para obtener más información, vea [SET ANSI_NULLS &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-ansi-nulls-transact-sql).  
  
 **Relleno ANSI habilitado**  
 Especifique si el relleno ANSI está activado o desactivado. Los valores permitidos son `True` (activado) y `False` (desactivado). Para obtener más información, vea [SET ANSI_PADDING &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-ansi-padding-transact-sql).  
  
 **Advertencias ANSI habilitadas**  
 Especifique el comportamiento estándar de ISO para diversas condiciones de error. Cuando `True`, se genera un mensaje de advertencia si aparecen valores null en funciones de agregado (como SUM, AVG, MAX, MIN, STDEV, STDEVP, VAR, VARP o COUNT). Cuando `False`, se genera ninguna advertencia. Para obtener más información, vea [SET ANSI_WARNINGS &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-ansi-warnings-transact-sql).  
  
 **Anulación aritmética habilitada**  
 Especifique si la opción de base de datos para la anulación aritmética está habilitada o deshabilitada. Los valores posibles son `True` y `False`. Cuando es `True`, un error de desbordamiento o de división por cero detendrá la consulta o el proceso por lotes. Si el error se produce en una transacción, esta se revierte. Cuando es `False`, aparece un mensaje de advertencia, pero la consulta, el proceso por lotes o la transacción continúa como si no se hubiera producido ningún error. Para obtener más información, vea [SET ARITHABORT &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-arithabort-transact-sql).  
  
 **Concatenar valores NULL produce NULL**  
 Especifique el comportamiento cuando se concatenan valores NULL. Cuando el valor de propiedad es `True`, `string` + NULL devuelve NULL. Cuando `False`, el resultado es `string`. Para obtener más información, vea [SET CONCAT_NULL_YIELDS_NULL &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-concat-null-yields-null-transact-sql).  
  
 **Encadenamiento de propiedad entre bases de datos habilitado**  
 Este valor de solo lectura indica si se ha habilitado el encadenamiento de propiedad entre bases de datos. Cuando `True`, la base de datos puede ser el origen o destino de una cadena de propiedad entre bases de datos. Utilice la instrucción ALTER DATABASE para establecer esta propiedad.  
  
 **Optimización de correlación de fechas habilitada**  
 Cuando `True`, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mantiene estadísticas de correlación entre dos tablas cualesquiera de la base de datos que estén vinculadas mediante una restricción FOREIGN KEY y tengan `datetime` columnas.  
  
 Cuando `False`, no se mantienen estadísticas de correlación.  
  
 **Anulación exacta numérica**  
 Especifique cómo controla la base de datos los errores de redondeo. Los valores posibles son `True` y `False`. Cuando es `True`, se genera un error si se produce una pérdida de precisión en una expresión. Cuando `False`, las pérdidas de precisión no generan mensajes de error y el resultado se redondea con la precisión de la columna o variable que lo almacena. Para obtener más información, vea [SET NUMERIC_ROUNDABORT &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-numeric-roundabort-transact-sql).  
  
 **Parametrización**  
 Cuando es **SIMPLE**, las consultas se parametrizan en función del comportamiento predeterminado de la base de datos. Cuando es **FORCED**, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] parametriza todas las consultas de la base de datos.  
  
 **Identificadores entre comillas habilitados**  
 Especifique si se pueden usar palabras clave de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como identificadores (un nombre de objeto o variable) si están delimitadas por comillas. Los valores posibles son `True` y `False`. Para obtener más información, vea [SET QUOTED_IDENTIFIER &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-quoted-identifier-transact-sql).  
  
 **Desencadenadores recursivos habilitados**  
 Especifique si los desencadenadores pueden activar otros desencadenadores. Los valores posibles son `True` y `False`. Cuando se establece en `True`, se habilita la activación recursiva de desencadenadores. Cuando se establece en `False`, solo se impide la recursividad directa. Para deshabilitar la repetición indirecta, establezca la opción nested triggers del servidor en 0 con sp_configure. Para obtener más información, vea [Crear desencadenadores anidado](../triggers/create-nested-triggers.md).  
  
 `Trustworthy`  
 Al mostrar `True`, esta opción de solo lectura indica que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permite el acceso a recursos externos a la base de datos en un contexto de suplantación establecido en la base de datos. Se pueden establecer contextos de suplantación dentro de la base de datos mediante la instrucción de usuario EXECUTE AS o la cláusula EXECUTE AS en módulos de base de datos.  
  
 Para obtener acceso, el propietario de la base de datos también debe disponer del permiso AUTHENTICATE SERVER en el nivel de servidor.  
  
 Esta propiedad también permite la creación y ejecución de ensamblados con acceso externo y no seguros dentro de la base de datos. Además de establecer esta propiedad en `True`, el propietario de la base de datos debe tener los permisos EXTERNAL ACCESS ASSEMBLY o UNSAFE ASSEMBLY en el nivel de servidor.  
  
 De forma predeterminada, todas las bases de datos de usuario y todas las bases de datos del sistema (con la excepción de **MSDB**) tienen esta propiedad establecida en `False`. No es posible cambiar este valor para las bases de datos **model** y **tempdb** .  
  
 TRUSTWORTHY se establece en `False` siempre que la base de datos se conecte al servidor.  
  
 El método recomendado para tener acceso a recursos externos a la base de datos en un contexto de suplantación es utilizar certificados y firmas, en lugar del `Trustworthy` opción.  
  
 Para establecer esta propiedad, utilice la instrucción ALTER DATABASE.  
  
 **Formato de almacenamiento VarDecimal habilitado**  
 Esta opción es de solo lectura a partir de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] y versiones posteriores, todas las bases de datos están habilitadas para el formato de almacenamiento vardecimal. Esta opción usa [sp_db_vardecimal_storage_format](/sql/relational-databases/system-stored-procedures/sp-db-vardecimal-storage-format-transact-sql).  
  
## <a name="recovery"></a>Recuperación  
 **Comprobación de páginas**  
 Especifique la opción utilizada para detectar y notificar las transacciones de E/S incompletas debido a errores de E/S de disco. Los valores posibles son **None**, **TornPageDetection**y **Checksum**. Para obtener más información, vea [Administrar la tabla suspect_pages &#40;SQL Server&#41;](../backup-restore/manage-the-suspect-pages-table-sql-server.md).  
  
 **Tiempo de recuperación de destino (segundos)**  
 Especifica el límite máximo de tiempo, expresado en segundos, para recuperar la base de datos especificada en caso de bloqueo. Para obtener más información, vea [Puntos de comprobación de base de datos &#40;SQL Server&#41;](../logs/database-checkpoints-sql-server.md).  
  
## <a name="state"></a>State  
 **Base de datos de solo lectura**  
 Especifica si la base de datos es de solo lectura. Los valores posibles son `True` y `False`. Cuando es `True`, los usuarios solo pueden leer los datos de la base de datos. Los usuarios no pueden modificar los objetos de datos ni de base de datos; sin embargo, la base de datos propiamente dicha se puede eliminar con la instrucción DROP DATABASE. La base de datos no puede estar en uso cuando se especifica un nuevo valor para la opción **Base de datos de solo lectura** . La base de datos maestra representa una excepción, y solo el administrador del sistema puede utilizar master mientras está habilitada la opción.  
  
 **Estado de la base de datos**  
 Muestra el estado actual de la base de datos. No se puede editar. Para obtener más información acerca del **Estado de base de datos**, vea [Database States](database-states.md).  
  
 **Restringir acceso**  
 Especifique los usuarios que pueden tener acceso a la base de datos. Los valores posibles son:  
  
-   **Varios**  
  
     El estado normal de una base de datos de producción; permite que varios usuarios tengan acceso a la base de datos a la vez.  
  
-   **Único**  
  
     Se utiliza en acciones de mantenimiento; solo un usuario puede tener acceso a la base de datos.  
  
-   **Restringido**  
  
     Solo los miembros de los roles db_owner, dbcreator o sysadmin pueden utilizar la base de datos.  
  
 **Cifrado habilitado**  
 Cuando `True`, esta base de datos está habilitada para el cifrado de base de datos. Se requiere el uso de una Clave de cifrado de base de datos. Para obtener más información, vea [Cifrado de datos transparente &#40;TDE&#41;](../security/encryption/transparent-data-encryption.md).  
  
## <a name="see-also"></a>Vea también  
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)   
 [CREATE DATABASE &#40;Transact-SQL de SQL Server&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql)  
  
  
