---
title: sp_OACreate (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_OACreate
- sp_OACreate_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_OACreate
ms.assetid: eb84c0f1-26dd-48f9-9368-13ee4a30a27c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5b7a56afb2ffa11dbe4ec8937efb602c13c9599d
ms.sourcegitcommit: 603d5ef9b45c2f111d36d11864dc032917e4a321
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/08/2019
ms.locfileid: "65450020"
---
# <a name="spoacreate-transact-sql"></a>sp_OACreate (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Crea una instancia de un objeto OLE.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_OACreate { progid | clsid } , objecttoken OUTPUT [ , context ]   
```  
  
## <a name="arguments"></a>Argumentos  
 *progid*  
 Es el identificador de programa (ProgID) del objeto OLE que se va a crear. Esta cadena de caracteres describe la clase del objeto OLE y tiene el formato: **'**_OLEComponent_**.** _Objeto_**'**  
  
 *OLEComponent* es el nombre del componente del servidor de automatización OLE, y *objeto* es el nombre del objeto OLE. El objeto OLE especificado debe ser válido y debe admitir la **IDispatch** interfaz.  
  
 Por ejemplo, SQLDMO. SQLServer es el ProgID de SQL-DMO **SQLServer** objeto. SQL-DMO tiene un nombre de componente de SQLDMO, el **SQLServer** objeto es válido y (como SQL-DMO todos los objetos de) la **SQLServer** admite **IDispatch**.  
  
 *clsid*  
 Es el identificador de clase (CLSID) del objeto OLE que se va a crear. Esta cadena de caracteres describe la clase del objeto OLE y tiene el formato: **' {**_nnnnnnnn-nnnn-nnnn-nnnn-nnnnnnnnnnnn_**}'**. El objeto OLE especificado debe ser válido y debe admitir la **IDispatch** interfaz.  
  
 Por ejemplo, {00026BA1-0000-0000-C000-000000000046} es el CLSID de SQL-DMO **SQLServer** objeto.  
  
 _objecttoken_ **OUTPUT**  
 Es el token de objeto devuelto, y debe ser una variable local del tipo de datos **int**. Este token de objeto identifica el objeto OLE creado y se utiliza en llamadas a otros procedimientos almacenados de OLE Automation.  
  
 *context*  
 Especifica el contexto de ejecución en que se ejecuta el objeto OLE recién creado. Si se especifica, este valor debe ser uno de los siguientes:  
  
 **1** = solo servidor OLE de proceso (.dll).  
  
 **4** = local (.exe) OLE solo servidor.  
  
 **5** = en curso y local servidores OLE  
  
 Si no se especifica, el valor predeterminado es **5**. Este valor se pasa como el *dwClsContext* parámetro de la llamada a **CoCreateInstance**.  
  
 Si se permite un servidor OLE de proceso (mediante el uso de un valor de contexto de **1** o **5** o si no especifica un valor de contexto), tiene acceso a la memoria y otros recursos que pertenecen a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Un servidor OLE de proceso interno puede dañar la memoria o los recursos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], y causar resultados imprevisibles, como una infracción de acceso a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Cuando se especifica un valor de contexto de **4**, un servidor OLE local no tiene acceso a cualquier [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] recursos y no se pueden dañar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] memoria o recursos.  
  
> [!NOTE]  
>  Los parámetros para este procedimiento almacenado se especifican por la posición, no por el nombre.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o un valor distinto de cero (error) que es el valor entero del HRESULT devuelto por el objeto de OLE Automation.  
  
 Para obtener más información sobre los códigos de retorno HRESULT, vea [OLE Automation códigos de retorno e información de Error](../../relational-databases/stored-procedures/ole-automation-return-codes-and-error-information.md).  
  
## <a name="remarks"></a>Comentarios  
 Si se habilitan los procedimientos de automatización OLE, una llamada a **sp_OACreate** iniciará el entorno de ejecución compartido OLE Automation. Para obtener más información acerca de cómo habilitar la automatización OLE, vea [Ole Automation procedimientos Server Configuration Option](../../database-engine/configure-windows/ole-automation-procedures-server-configuration-option.md).  
  
 El objeto OLE creado se destruye automáticamente al final del lote de instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
## <a name="permissions"></a>Permisos  
 Debe pertenecer a la **sysadmin** rol fijo de servidor o permiso de ejecución directamente en este procedimiento almacenado. `Ole Automation Procedures` configuración de debe ser **habilitado** utilizar ningún procedimiento del sistema relacionadas con la automatización OLE.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-using-progid"></a>A. Utilizar ProgID  
 En el ejemplo siguiente se crea un SQL-DMO **SQLServer** objeto mediante su ProgID.  
  
```  
DECLARE @object int;  
DECLARE @hr int;  
DECLARE @src varchar(255), @desc varchar(255);  
EXEC @hr = sp_OACreate 'SQLDMO.SQLServer', @object OUT;  
IF @hr <> 0  
BEGIN  
   EXEC sp_OAGetErrorInfo @object, @src OUT, @desc OUT   
   raiserror('Error Creating COM Component 0x%x, %s, %s',16,1, @hr, @src, @desc)  
    RETURN  
END;  
GO  
```  
  
### <a name="b-using-clsid"></a>b. Utilizar CLSID  
 En el ejemplo siguiente se crea un SQL-DMO **SQLServer** objeto mediante su CLSID.  
  
```  
DECLARE @object int;  
DECLARE @hr int;  
DECLARE @src varchar(255), @desc varchar(255);  
EXEC @hr = sp_OACreate '{00026BA1-0000-0000-C000-000000000046}',  
    @object OUT;  
IF @hr <> 0  
BEGIN  
   EXEC sp_OAGetErrorInfo @object, @src OUT, @desc OUT   
   raiserror('Error Creating COM Component 0x%x, %s, %s',16,1, @hr, @src, @desc)  
    RETURN  
END;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [OLE Automation procedimientos almacenados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/ole-automation-stored-procedures-transact-sql.md)   
 [Opción de configuración de servidor de procedimientos de OLE Automation](../../database-engine/configure-windows/ole-automation-procedures-server-configuration-option.md)   
 [Ejemplo de script de automatización OLE](../../relational-databases/stored-procedures/ole-automation-sample-script.md)  
  
  
