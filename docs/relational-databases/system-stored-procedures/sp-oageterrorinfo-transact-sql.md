---
title: sp_OAGetErrorInfo (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_OAGetErrorInfo_TSQL
- sp_OAGetErrorInfo
dev_langs:
- TSQL
helpviewer_keywords:
- sp_OAGetErrorInfo
ms.assetid: ceecea08-456f-4819-85d9-ecc9647d7187
caps.latest.revision: 16
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: b272cbcc6fc8221dede3b4a1274032926910186a
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
---
# <a name="spoageterrorinfo-transact-sql"></a>sp_OAGetErrorInfo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Obtiene información de errores de OLE Automation.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_OAGetErrorInfo [ objecttoken ]  
    [ , source OUTPUT ]   
    [ , description OUTPUT ]   
    [ , helpfile OUTPUT ]   
    [ , helpid OUTPUT ]   
```  
  
## <a name="arguments"></a>Argumentos  
 *objecttoken*  
 Es el token de acceso objeto de un objeto OLE que se creó previamente mediante **sp_OACreate** o es NULL. Si *objecttoken* está especificado, se devuelve información de error para ese objeto. Si se especifica NULL, se devuelve la información de error de todo el lote.  
  
 *origen* **salida**  
 Es el origen de la información de error. Si se especifica, debe ser una variable local **char**, **nchar**, **varchar**, o **nvarchar** variable. El valor devuelto se trunca, si es necesario, para que se ajuste a la variable local.  
  
 *descripción* **salida**  
 Es la descripción del error. Si se especifica, debe ser una variable local **char**, **nchar**, **varchar**, o **nvarchar** variable. El valor devuelto se trunca, si es necesario, para que se ajuste a la variable local.  
  
 *HelpFile* **salida**  
 Es el archivo de ayuda del objeto OLE. Si se especifica, debe ser una variable local **char**, **nchar**, **varchar**, o **nvarchar** variable. El valor devuelto se trunca, si es necesario, para que se ajuste a la variable local.  
  
 *HelpID* **salida**  
 Es el identificador de contexto del archivo de ayuda. Si se especifica, debe ser una variable local **int** variable.  
  
> [!NOTE]  
>  Los parámetros para este procedimiento almacenado se especifican por la posición, no por el nombre.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o un valor distinto de cero (error) que es el valor entero del HRESULT devuelto por el objeto de OLE Automation.  
  
 Para obtener más información sobre códigos de retorno HRESULT, vea [OLE Automation códigos de retorno e información de Error](../../relational-databases/stored-procedures/ole-automation-return-codes-and-error-information.md).  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Si no se especifican parámetros de salida, la información de error se devuelve al cliente como un conjunto de resultados.  
  
|Nombres de columna|Tipo de datos|Description|  
|------------------|---------------|-----------------|  
|**Error**|**binary (4)**|Representación binaria del número de error.|  
|**Source**|**nvarchar(nn)**|Origen del error.|  
|**Description**|**nvarchar(nn)**|Descripción del error.|  
|**HelpFile**|**nvarchar(nn)**|Archivo de ayuda del origen.|  
|**HelpID**|**int**|Id. del contexto de Ayuda del archivo de origen correspondiente.|  
  
## <a name="remarks"></a>Comentarios  
 Procedimiento almacenado de cada llamada a una automatización OLE (excepto **sp_OAGetErrorInfo**) restablece la información de error; por lo tanto, **sp_OAGetErrorInfo** obtiene información de errores únicamente para la última OLE Automatización de la llamada al procedimiento almacenado. Tenga en cuenta que, dado que **sp_OAGetErrorInfo** no restablece la información de error, puede llamarse varias veces para obtener la misma información de error.  
  
 La tabla siguiente muestra los errores de OLE Automation y sus causas comunes.  
  
|Error y HRESULT|Causa común|  
|-----------------------|------------------|  
|**Tipo de variable incorrecto (0 x 80020008)**|Tipo de datos de un [!INCLUDE[tsql](../../includes/tsql-md.md)] valor pasado como un parámetro de método no coincidía con el [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] tipo de datos del parámetro del método o un valor NULL se pasó como un parámetro de método.|  
|**¿Nombre desconocido (0 x 8002006)**|No se encontró el nombre de la propiedad o del método especificado para el objeto especificado.|  
|**Cadena de clase no válida (0x800401f3)**|El ProgID o CLSID especificado no está registrado como objeto OLE en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Los servidores de automatización OLE personalizados deben estar registrados puede instanciarse mediante **sp_OACreate**. Esto puede hacerse mediante la utilidad Regsvr32.exe para los servidores de proceso (.dll), o la **/regserver** conmutador de línea de comandos para servidores locales (.exe).|  
|**Error de ejecución del servidor (0 x 80080005)**|El objeto OLE especificado está registrado como servidor OLE local (archivo .exe), pero no se pudo encontrar o iniciar el archivo .exe.|  
|**El módulo especificado no se encontró (0x8007007e)**|El objeto OLE especificado está registrado como servidor OLE en proceso (archivo .dll), pero no se pudo encontrar o cargar el archivo .dll.|  
|**Error de coincidencia de tipo (0 x 80020005)**|El tipo de datos de una variable local de [!INCLUDE[tsql](../../includes/tsql-md.md)] utilizada para almacenar un valor de propiedad o un valor de método devueltos no coincidió con el tipo de datos de [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] para el valor devuelto de la propiedad o método. O bien, se solicitó el valor devuelto de una propiedad o método, pero no se devuelve un valor.|  
|**El tipo de datos o el valor del parámetro 'context' de sp_OACreate no es válido. (0x8004275B)**|El valor del parámetro de contexto debe ser uno de los siguientes: 1, 4 o 5.|  
  
 Para obtener más información acerca de cómo procesar códigos de retorno HRESULT, vea [OLE Automation códigos de retorno e información de Error](../../relational-databases/stored-procedures/ole-automation-return-codes-and-error-information.md).  
  
## <a name="permissions"></a>Permissions  
 Requiere la pertenencia al rol fijo de servidor **sysadmin** .  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente muestra la información de errores de OLE Automation.  
  
```  
DECLARE @output varchar(255);  
DECLARE @hr int;  
DECLARE @source varchar(255);  
DECLARE @description varchar(255);  
PRINT 'OLE Automation Error Information';  
EXEC @hr = sp_OAGetErrorInfo @object, @source OUT, @description OUT;  
IF @hr = 0  
BEGIN  
    SELECT @output = '  Source: ' + @source  
    PRINT @output  
    SELECT @output = '  Description: ' + @description  
    PRINT @output  
END  
ELSE  
BEGIN  
    PRINT '  sp_OAGetErrorInfo failed.'  
    RETURN  
END;  
```  
  
## <a name="see-also"></a>Vea también  
 [OLE procedimientos almacenados de automatización &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/ole-automation-stored-procedures-transact-sql.md)   
 [Ejemplo de script de automatización OLE](../../relational-databases/stored-procedures/ole-automation-sample-script.md)  
  
  
