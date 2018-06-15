---
title: sp_copysubscription (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_copysubscription
- sp_copysubscription_TSQL
helpviewer_keywords:
- sp_copysubscription
ms.assetid: 3c56cd62-2966-4e87-a986-44cb3fd0b760
caps.latest.revision: 33
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 3cae06562e37cf10c2fa94934eedb20880b4391a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32993222"
---
# <a name="spcopysubscription-transact-sql"></a>sp_copysubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

    
> [!IMPORTANT]  
>  La característica de suscripciones adjuntables ha quedado desusada y se retirará en versiones posteriores. Esta característica no se debe utilizar en nuevos trabajos de desarrollo. En las publicaciones de combinación en las que se han creado particiones mediante filtros con parámetros, se recomienda utilizar las nuevas características de las instantáneas con particiones, que simplifican la inicialización de un gran número de suscripciones. Para más información, consulte [Snapshots for Merge Publications with Parameterized Filters](../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md). En las publicaciones que no están divididas en particiones, puede inicializar una suscripción con una copia de seguridad. Para obtener más información, consulte [Initialize a Transactional Subscription Without a Snapshot](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md).  
  
 Copia una base de datos de suscripciones que tiene suscripciones de extracción, pero no de inserción. Solo se pueden copiar bases de datos de un único archivo. Este procedimiento almacenado se ejecuta en el suscriptor de la base de datos de suscripción.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_copysubscription [ @filename = ] 'file_name'  
    [ , [ @temp_dir = ] 'temp_dir' ]  
    [ , [ @overwrite_existing_file = ] overwrite_existing_file]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@filename =**] **'***file_name***'**  
 Es la cadena que especifica la ruta de acceso completa, incluido el nombre de archivo, donde se guardará una copia del archivo de datos (.mdf). *nombre de archivo* es **nvarchar (260)**, no tiene ningún valor predeterminado.  
  
 [  **@temp_dir=**] **'***temp_dir***'**  
 Es el nombre del directorio que contiene los archivos temporales. *temp_dir* es **nvarchar (260)**, su valor predeterminado es null. Si es NULL, el [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se utilizará el directorio de datos predeterminado. El directorio debe tener espacio suficiente para contener un archivo que tenga el tamaño de todos los archivos de la base de datos del suscriptor combinados.  
  
 [  **@overwrite_existing_file=**] **'***overwrite_existing_file***'**  
 Es una marca booleana opcional que especifica si se debe o no sobrescribir un archivo existente del mismo nombre especificado en **@filename**. *overwrite_existing_file*es **bits**, su valor predeterminado es **0**. Si **1**, sobrescribe el archivo especificado por **@filename**, si existe. Si **0**, el procedimiento almacenado produce un error si el archivo existe y no se sobrescribe el archivo.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_copysubscription** se utiliza en todos los tipos de replicación para copiar una base de datos de suscripción a un archivo como alternativa al aplicar la instantánea en el suscriptor. La base de datos se debe configurar para que solo admita suscripciones de extracción. Los usuarios que tengan los permisos apropiados pueden realizar copias de la base de datos de suscripciones y, a continuación, enviar por correo electrónico, copiar o transportar el archivo de suscripción (.msf) a otro suscriptor, donde se puede adjuntar como una suscripción.  
  
 El tamaño de la base de datos de suscripciones que se va a copiar debe ser inferior a 2 gigabytes (GB).  
  
 **sp_copysubscription** solo se admite para bases de datos con las suscripciones de cliente y no se puede ejecutar cuando la base de datos tiene suscripciones de servidor.  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros de la **sysadmin** rol fijo de servidor puede ejecutar **sp_copysubscription**.  
  
## <a name="see-also"></a>Vea también  
 [Ubicaciones alternativas para las carpetas de instantáneas](../../relational-databases/replication/alternate-snapshot-folder-locations.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
