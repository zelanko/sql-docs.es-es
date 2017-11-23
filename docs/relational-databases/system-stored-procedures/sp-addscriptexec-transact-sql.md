---
title: sp_addscriptexec (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- sp_addscriptexec
- sp_addscriptexec_TSQL
helpviewer_keywords: sp_addscriptexec
ms.assetid: 1627db41-6a80-45b6-b0b9-c0b7f9a1c886
caps.latest.revision: "27"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 13f3104f91c785252f573e653d3344a03091dd13
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="spaddscriptexec-transact-sql"></a>sp_addscriptexec (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Expone un script SQL (archivo .sql) para todos los suscriptores de una publicación. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_addscriptexec [ @publication = ] publication  
    [ , [ @scriptfile = ] 'scriptfile' ]  
    [ , [ @skiperror = ] 'skiperror' ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publication=** ] **'***publicación***'**  
 Es el nombre de la publicación. *publicación* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@scriptfile=** ] **'***scriptfile***'**  
 Es la ruta de acceso completa al archivo de script SQL. *ScriptFile* es **nvarchar (4000)**, no tiene ningún valor predeterminado.  
  
 [  **@skiperror=** ] **'***skiperror***'**  
 Indica si el Agente de distribución o el Agente de mezcla se debe detener cuando se encuentra un error durante el procesamiento de script. *SkipError* es **bits**, con un valor predeterminado es 0.  
  
 **0** = el agente se detendrá.  
  
 **1** = el agente continúa la secuencia de comandos y pasa por alto el error.  
  
 [  **@publisher=** ] **'***publisher***'**  
 Especifica un no[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publisher. *Publisher* es **sysname**, su valor predeterminado es null.  
  
> [!NOTE]  
>  *Publisher* no debe usarse al publicar desde una [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publisher.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_addscriptexec** se utiliza en la replicación transaccional de replicación y de mezcla.  
  
 **sp_addscriptexec** no se utiliza para la replicación de instantáneas.  
  
 Usar **sp_addscriptexec**, la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cuenta de servicio debe tener de lectura y se almacenan los permisos de escritura en los permisos de lectura y de ubicación de instantánea en la ubicación donde las secuencias de comandos.  
  
 El [utilidad sqlcmd](../../tools/sqlcmd-utility.md) se usa para ejecutar el script en el suscriptor, y el script se ejecuta en el contexto de seguridad utilizado por el agente de distribución o el agente de mezcla al conectarse a la base de datos de suscripción. Cuando el agente se ejecuta en una versión anterior de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], [utilidad osql](../../tools/osql-utility.md) se utiliza en lugar de [sqlcmd](../../tools/sqlcmd-utility.md).  
  
 **sp_addscriptexec** es muy útil para aplicar secuencias de comandos a los suscriptores y usa [sqlcmd](../../tools/sqlcmd-utility.md) para aplicar el contenido de la secuencia de comandos en el suscriptor. No obstante, dado que las configuraciones del suscriptor pueden variar, los scripts probados antes de enviarlos al publicador también pueden generar errores en un suscriptor. *SkipError* ofrece la posibilidad de que el agente de distribución o agente de mezcla omita los errores y continúe. Use [sqlcmd](../../tools/sqlcmd-utility.md) para probar los scripts antes de ejecutar **sp_addscriptexec**.  
  
> [!NOTE]  
>  Los errores omitidos se registran en el historial del agente como referencia.  
  
 Usar **sp_addscriptexec** para registrar un archivo de script para usar FTP para una entrega la instantánea solo se admite para las publicaciones [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] los suscriptores.  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros de la **sysadmin** rol fijo de servidor o **db_owner** rol fijo de base de datos puede ejecutar **sp_addscriptexec**.  
  
## <a name="see-also"></a>Vea también  
 [Ejecutar Scripts durante la sincronización &#40; Programación de replicación Transact-SQL &#41;](../../relational-databases/replication/execute-scripts-during-synchronization-replication-transact-sql-programming.md)   
 [Synchronize Data](../../relational-databases/replication/synchronize-data.md)  (Sincronizar datos)  
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
