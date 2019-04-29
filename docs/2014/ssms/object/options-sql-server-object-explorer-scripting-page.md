---
title: Opciones (página Scripting en el Explorador de objetos de SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.ObjectExplorerScripting
- VS.ToolsOptionsPages.Sql_Server_Object_Explorer.ObjectExplorerScripting
ms.assetid: 6105aec9-1b72-4cb2-bd24-fc35f6d95240
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 81e4bafbd596894a8cecbeb707a5d8be698c1f3b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63031939"
---
# <a name="options-sql-server-object-explorer-scripting-page"></a>Opciones (página Scripting en el Explorador de objetos de SQL Server)
  Use esta página para establecer las opciones de scripting que se aplican a los siguientes comandos en los menús contextuales de objetos del **Explorador de objetos**:  
  
-   Comandos **Editar** para las tablas y vistas del usuario.  
  
-   **Secuencia de comandos \<objeto > como** comandos para los objetos creados por el usuario.  
  
-   Comando **Modificar** para los objetos creados por el usuario.  
  
-   Esta página también establece los valores predeterminados de las opciones de scripting del **Asistente para generar scripts de SQL Server**.  
  
## <a name="remarks"></a>Comentarios  
 El **editar** y **modificar** comandos podrían producir resultados diferentes de los **Script \<objeto > como** el comando para el mismo valor de opción. Los comandos **Editar** y **Modificar** están diseñados para modificar objetos en la base de datos actual durante una sesión del Editor de consultas. El **Script \<objeto > como** comando está diseñado para generar un script que se puede usar posteriormente para crear objetos.  
  
## <a name="options"></a>Opciones  
 Para especificar las opciones de scripts, seleccione las opciones de configuración disponibles en la lista situada a la derecha de cada opción.  
  
### <a name="general-scripting-options"></a>Opciones generales de scripting  
 **Delimitar instrucciones individuales**  
 Separa instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] individuales mediante un separador de lotes. Para cambiar el separador de lotes predeterminado del **Editor de consultas**, seleccione **Herramientas**/**Opciones**/**Ejecución de la consulta**/**SQL Server**/**General**/**Separador de lotes**. El valor predeterminado es False. Para obtener más información, consulte [vaya &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/sql-server-utilities-statements-go).  
  
 **Incluir encabezados descriptivos**  
 Agrega comentarios descriptivos al script dividiéndolo en secciones para cada objeto. El valor predeterminado es True. Para obtener más información, consulte [comentario &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/comment-transact-sql).  
  
 **Incluir opciones vardecimal**  
 Incluye las opciones de almacenamiento vardecimal. El valor predeterminado es False. Para obtener más información, vea y [sp_db_vardecimal_storage_format &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-db-vardecimal-storage-format-transact-sql).  
  
 **Crear scripts para el historial de cambios**  
 Incluye información del historial de cambios en el script.  
  
 **Script para versión de servidor**  
 Crea un script que se puede ejecutar en la versión seleccionada de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Las características nuevas de [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] no se pueden incluir en scripts para versiones anteriores. Algunos scripts creados para [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] no pueden ejecutarse en servidores que ejecutan una versión anterior de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]o en una base de datos con un [valor de nivel de compatibilidad de base de datos](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level)anterior.  
  
 **Generar script de catálogos de texto completo**  
 Incluye un script para catálogos de texto completo. El valor predeterminado es False. Para obtener más información, consulte [CREATE FULLTEXT CATALOG &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-catalog-transact-sql).  
  
 **USO de secuencias de comandos \<base de datos >**  
 Agrega la instrucción USE DATABASE al script para crear objetos de base de datos en el contexto de la base de datos actual del **Explorador de objetos** . Cuando necesite usar el script en otra base de datos, seleccione False para omitir. El valor predeterminado es True. Para obtener más información, vea [USE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/use-transact-sql).  
  
### <a name="object-scripting-options"></a>Opciones de scripting de objetos  
 **Generar script para objetos dependientes**  
 Genera un script para objetos adicionales que son necesarios cuando se ejecuta el script para el objeto seleccionado. El valor predeterminado es False.  
  
 **Incluir cláusula IF NOT EXISTS**  
 Incluye una instrucción para comprobar que los objetos no existen en la base de datos antes de intentar crear el objeto. El valor predeterminado es False. Para obtener más información, consulte [IF... ELSE &#40;Transact-SQL&#41; ](/sql/t-sql/language-elements/if-else-transact-sql) y [EXISTS &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/exists-transact-sql).  
  
 **Nombres de objeto de certificación de esquema**  
 Califica nombres de objeto con el esquema de objetos. El valor predeterminado es False. Para más información, consulte [Crear un esquema de base de datos](../../relational-databases/security/authentication-access/create-a-database-schema.md).  
  
 **Generar script de propiedades extendidas**  
 Incluye propiedades extendidas en el script si el objeto tiene propiedades extendidas. El valor predeterminado es False. Para obtener más información, vea [sp_addextendedproperty &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addextendedproperty-transact-sql).  
  
 **Incluir propietario**  
 Incluye el propietario en el script generado. El valor predeterminado es False.  
  
 **Generar script de permisos**  
 Incluye permisos sobre los objetos de la base de datos en el script. El valor predeterminado es True. Para obtener más información, consulte [permisos &#40;motor de base de datos&#41;](../../relational-databases/security/permissions-database-engine.md).  
  
### <a name="tableview-options"></a>Opciones de tabla o vista  
 Las siguientes opciones solo se aplican a scripts para tablas o vistas.  
  
 **Convertir tipos de datos definidos por el usuario en tipos base**  
 Convierte los tipos de datos definidos por el usuario en los tipos base a partir de los cuales se crearon. Utilice el valor True cuando los tipos de datos definidos por el usuario de la base de datos de origen no existan en la base de datos en la que se va a ejecutar el script. Utilice el valor False para mantener los tipos de datos definidos por el usuario. El valor predeterminado es False. Para obtener más información, consulte [CREATE TYPE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-type-transact-sql).  
  
 **Generar comandos SET ANSI PADDING**  
 Agrega la instrucción SET ANSI_PADDING antes y después de cada instrucción CREATE TABLE. El valor predeterminado es True. Para obtener más información, vea [SET ANSI_PADDING &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-ansi-padding-transact-sql).  
  
 **Incluir intercalación**  
 Incluye una intercalación en la definición de columna. El valor predeterminado es True. Para más información, consulte [Compatibilidad con la intercalación y Unicode](../../relational-databases/collations/collation-and-unicode-support.md).  
  
 **Incluir propiedad IDENTITY**  
 Incluye definiciones para el valor de inicialización IDENTITY y el incremento IDENTITY. El valor predeterminado es True. Para obtener más información, vea [IDENTITY &#40;propiedad &#41; &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-table-transact-sql-identity-property).  
  
 **Referencias de claves externas de certificación de esquema**  
 Agrega el nombre de esquema a las referencias de tabla para las restricciones FOREIGN KEY. El valor predeterminado es True.  
  
 **Generar script de reglas y valores predeterminados enlazados**  
 Incluye las llamadas a los procedimientos almacenados enlazados **sp_bindefault** y **sp_bindrule** . El valor predeterminado es True. Para obtener más información, consulte [sp_bindefault &#40;Transact-SQL&#41; ](/sql/relational-databases/system-stored-procedures/sp-bindefault-transact-sql) y [sp_bindrule &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-bindrule-transact-sql).  
  
 **Generar script de restricciones CHECK**  
 Agrega [restricciones CHECK](../../relational-databases/tables/unique-constraints-and-check-constraints.md) al script. El valor predeterminado es True.  
  
 **Incluir valores predeterminados**  
 Incluye valores predeterminados de columna en el script. El valor predeterminado es False. Para obtener más información, vea [CREATE DEFAULT &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-default-transact-sql).  
  
 **Generar script de grupos de archivos**  
 Especifica el grupo de archivos en la cláusula ON para definiciones de tabla. El valor predeterminado es False. Para obtener más información, vea [CREATE TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-table-transact-sql).  
  
 **Incluir claves externas en el script**  
 Incluye [restricciones FOREIGN KEY](../../relational-databases/tables/primary-and-foreign-key-constraints.md) en el script. El valor predeterminado es False.  
  
 **Incluir índices de texto completo**  
 Incluye índices de texto completo en el script. El valor predeterminado es False. Para obtener más información, consulte [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-index-transact-sql).  
  
 **Incluir índices en el script**  
 Incluye índices clúster, no clúster y XML en el script. El valor predeterminado es True. Para obtener más información, vea [CREATE INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-index-transact-sql).  
  
 **Generar script de esquemas de partición**  
 Incluye esquemas de particiones de tabla en el script. El valor predeterminado es False. Para obtener más información, consulte [CREATE PARTITION SCHEME &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-partition-scheme-transact-sql).  
  
 **Incluir claves principales en el script**  
 Incluye [Restricciones entre claves principales y claves externas](../../relational-databases/tables/primary-and-foreign-key-constraints.md) en el script. El valor predeterminado es True.  
  
 **Incluir estadísticas en el script**  
 Incluye estadísticas definidas por el usuario en el script. El valor predeterminado es False. Para obtener más información, vea [CREATE STATISTICS &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-statistics-transact-sql).  
  
 **Incluir desencadenadores**  
 Incluye desencadenadores en el script. El valor predeterminado es False. Para obtener más información, vea [CREATE TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-trigger-transact-sql).  
  
 **Incluir claves únicas en el script**  
 Incluye [Restricciones UNIQUE y restricciones CHECK](../../relational-databases/tables/unique-constraints-and-check-constraints.md) en el script. El valor predeterminado es False.  
  
 **Generar script de columnas de vista**  
 Declara columnas de vista en encabezados de vista. El valor predeterminado es False. Para obtener más información, vea [CREATE VIEW &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-view-transact-sql).  
  
 **ScriptDriIncludeSystemNames**  
 Incluye nombres de restricción generados por el sistema para aplicar la integridad referencial declarativa. El valor predeterminado es False. Para obtener más información, consulte [REFERENTIAL_CONSTRAINTS &#40;Transact-SQL&#41;](/sql/relational-databases/system-information-schema-views/referential-constraints-transact-sql).  
  
## <a name="see-also"></a>Vea también  
 [Generar scripts &#40;SQL Server Management Studio&#41;](../../relational-databases/scripting/generate-scripts-sql-server-management-studio.md)  
  
  
