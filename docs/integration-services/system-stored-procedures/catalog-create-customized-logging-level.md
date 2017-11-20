---
title: Catalog.create_customized_logging_level | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 20b3ba0a-126f-49bf-b70f-61b2a0fcb750
caps.latest.revision: 9
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 126fa0af811033bb0be035b1f4c550620c696bb3
ms.contentlocale: es-es
ms.lasthandoff: 09/26/2017

---
# <a name="catalogcreatecustomizedlogginglevel"></a>Catalog.create_customized_logging_level
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Crea un nuevo nivel de registro personalizados. Para obtener más información acerca de los niveles de registro personalizados, consulte [Integration Services &#40; SSIS &#41; Registro](../../integration-services/performance/integration-services-ssis-logging.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```sql  
catalog.create_customized_logging_level [ @level_name = ] level_name  
    , [ @level_description = ] level_description  
    , [ @profile_value = ] profile_value  
    , [ @event_value = ] event_value  
    , [ @level_id = ] level_id OUT   
```  
  
## <a name="arguments"></a>Argumentos  
 [ @level_name =] *level_name*  
 El nombre para el contexto del nuevo nivel de registro personalizado.  
  
 El *level_name* es **nvarchar (128)**.  
  
 [ @level_description =] *level_description*  
 Nivel de registro personalizado de la descripción del nuevo ya existentes.  
  
 El *level_description* es **nvarchar (1024)**.  
  
 [ @profile_value =] *profile_value*  
 Las estadísticas que desea que el nuevo nivel de registro para iniciar una sesión de personalizado.  
  
 Los valores válidos para las estadísticas incluyen lo siguiente. Estos valores se corresponden con los valores en el **estadísticas** pestaña de la **personalizar administración de nivel de registro** cuadro de diálogo.  
  
-   Ejecución = 0  
  
-   Volumen = 1  
  
-   Rendimiento = 2  
  
 El *profile_value* es un **bigint**.  
  
 [ @event_value =] *event_value*  
 Los eventos que desea que el nuevo nivel de registro para iniciar una sesión de personalizado.  
  
 Los valores válidos para los eventos incluyen lo siguiente. Estos valores se corresponden con los valores en el **eventos** pestaña de la **personalizar administración de nivel de registro** cuadro de diálogo.  
  
|Eventos sin contexto del evento|Eventos con el contexto del evento|  
|----------------------------------|-------------------------------|  
|OnVariableValueChanged = 0<br /><br /> OnExecutionStatusChanged = 1<br /><br /> OnPreExecute = 2<br /><br /> OnPostExecute = 3<br /><br /> OnPreValidate = 4<br /><br /> OnPostValidate = 5<br /><br /> OnWarning = 6<br /><br /> OnInformation = 7<br /><br /> OnError = 8<br /><br /> OnTaskFailed = 9<br /><br /> OnProgress = 10<br /><br /> OnQueryCancel = 11<br /><br /> OnBreakpointHit = 12<br /><br /> OnCustomEvent = 13<br /><br /> Diagnóstico = 14<br /><br /> DiagnosticEx = 15<br /><br /> NonDiagnostic = 16|OnVariableValueChanged_IncludeContext = 32<br /><br /> OnExecutionStatusChanged_IncludeContext = 33<br /><br /> OnPreExecute_IncludeContext = 34<br /><br /> OnPostExecute_IncludeContext = 35<br /><br /> OnPreValidate_IncludeContext = 36<br /><br /> OnPostValidate_IncludeContext = 37<br /><br /> OnWarning_IncludeContext = 38<br /><br /> OnInformation_IncludeContext = 39<br /><br /> OnError_IncludeContext = 40<br /><br /> OnTaskFailed_IncludeContext = 41<br /><br /> OnProgress_IncludeContext = 42<br /><br /> OnQueryCancel_IncludeContext = 43<br /><br /> OnBreakpointHit_IncludeContext = 44<br /><br /> OnCustomEvent_IncludeContext = 45<br /><br /> Diagnostic_IncludeContext = 46<br /><br /> DiagnosticEx_IncludeContext = 47<br /><br /> NonDiagnostic_IncludeContext = 48|  
  
 El *event_value* es un **bigint**.  
  
 [ @level_id =] *level_id* OUT  
 El identificador del nuevo nivel de registro personalizado.  
  
 El *level_id* es un **bigint**.  
  
## <a name="remarks"></a>Comentarios  
 Para combinar varios valores de Transact-SQL para la *profile_value* o *event_value* argumento, siga este ejemplo. Para capturar las OnError (8) y los eventos de DiagnosticEx (15), la fórmula para calcular *event_value* es `2^8 + 2^15 = 33024`.  
  
## <a name="return-codes"></a>Códigos de retorno  
 0 (correcto)  
  
 Cuando se produce un error en el procedimiento almacenado, se genera un error.  
  
## <a name="result-set"></a>Conjunto de resultados  
 Ninguno  
  
## <a name="permissions"></a>Permissions  
 Este procedimiento almacenado necesita uno de los permisos siguientes:  
  
-   Pertenencia al rol de base de datos **ssis_admin**  
  
-   Pertenencia al rol de servidor **sysadmin**  
  
## <a name="errors-and-warnings"></a>Errores y advertencias  
 En la lista siguiente se describen las condiciones que hacen que el procedimiento almacenado genere un error.  
  
-   El usuario no tiene los permisos necesarios.  
  
  

