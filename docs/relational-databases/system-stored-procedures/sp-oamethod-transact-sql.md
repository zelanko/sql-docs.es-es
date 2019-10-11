---
title: sp_OAMethod (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_OAMethod
- sp_OAMethod_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_OAMethod
ms.assetid: 1dfaebe2-c7cf-4041-a586-5d04faf2e25e
author: stevestein
ms.author: sstein
ms.openlocfilehash: 7f0196a710f9349e109bcf956eca6e2310c1e051
ms.sourcegitcommit: c426c7ef99ffaa9e91a93ef653cd6bf3bfd42132
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/10/2019
ms.locfileid: "72252197"
---
# <a name="sp_oamethod-transact-sql"></a>sp_OAMethod (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Llama a un método de un objeto OLE.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_OAMethod objecttoken , methodname  
    [ , returnvalue OUTPUT ]   
    [ , [ @parametername = ] parameter [ OUTPUT ] [ ...n ] ]   
```  
  
## <a name="arguments"></a>Argumentos  
 *objecttoken*  
 Es el token de objeto de un objeto OLE creado previamente con **sp_OACreate**.  
  
 *MethodName*  
 Es el nombre de método del objeto OLE al que se llamará.  
  
 **salida** ReturnValue  
 Es el valor devuelto del método del objeto OLE. Si se especifica, debe ser una variable local del tipo de datos adecuado.  
  
 Si el método devuelve un valor único, especifique una variable local para *ReturnValue*, que devuelve el valor devuelto por el método en la variable local, o no especifique *ReturnValue*, que devuelve el valor devuelto por el método al cliente como conjunto de resultados de una sola fila y una sola columna.  
  
 Si el valor devuelto del método es un objeto OLE, *ReturnValue* debe ser una variable local de tipo de datos **int**. En la variable local se almacena un token de objeto que se puede utilizar con otros procedimientos almacenados de OLE Automation.  
  
 Cuando el valor devuelto del método es una matriz, si se especifica *ReturnValue* , se establece en NULL.  
  
 Se genera un error si se da uno de los casos siguientes:  
  
-   se especifica *ReturnValue* , pero el método no devuelve un valor.  
  
-   El método devuelve una matriz con más de dos dimensiones.  
  
-   El método devuelve una matriz como parámetro de salida.  
  
`[ _@parametername = ] parameter[ OUTPUT ]` es un parámetro de método. Si se especifica, el *parámetro* debe ser un valor del tipo de datos adecuado.  
  
 Para obtener el valor devuelto de un parámetro de salida, el *parámetro* debe ser una variable local del tipo de datos adecuado y se debe especificar **Output** . Si se especifica un parámetro constante, o si no se especifica **Output** , se omite cualquier valor devuelto de un parámetro de salida.  
  
 Si se especifica, *parameterName* debe ser el nombre del parámetro con nombre [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]. Tenga en cuenta que **@** _parametername_is no es una variable local de @no__t 2. Se quita el signo de arroba ( **@** ) y *parameterName*se pasa al objeto OLE como el nombre del parámetro. Todos los parámetros con nombre deben especificarse después de especificar todos los parámetros de posición.  
  
 *n*  
 Es un marcador de posición que indica que se pueden especificar varios parámetros.  
  
> [!NOTE]
>  *\@parametername* puede ser un parámetro con nombre porque forma parte del método especificado y se pasa a través del objeto. Los demás parámetros de este procedimiento almacenado se especifican por la posición, no por el nombre.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o un valor distinto de cero (error) que es el valor entero del HRESULT devuelto por el objeto de OLE Automation.  
  
 Para obtener más información acerca de los códigos de retorno de HRESULT, [códigos de retorno e información de error de automatización OLE](../../relational-databases/stored-procedures/ole-automation-return-codes-and-error-information.md).  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Si el valor devuelto del método es una matriz con una o dos dimensiones, se devuelve la matriz al cliente como un conjunto de resultados:  
  
-   Se devuelve al cliente una matriz unidimensional como conjunto de resultados de fila única con tantas columnas como elementos tenga la matriz. Es decir, la matriz se devuelve como (columnas).  
  
-   Se devuelve al cliente una matriz bidimensional como conjunto de resultados con tantas columnas como elementos haya en la primera dimensión de la matriz y con tantas filas como elementos haya en la segunda dimensión de la matriz. En otras palabras, la matriz se devuelve como (columnas, filas).  
  
 Cuando un valor devuelto por una propiedad o un método es una matriz, **sp_OAGetProperty** o **sp_OAMethod** devuelven un conjunto de resultados al cliente. (Los parámetros de salida del método no pueden ser matrices.) Estos procedimientos recorren todos los valores de datos de la matriz para determinar los tipos de datos y las longitudes de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] adecuados para cada columna del conjunto de resultados. Para una columna determinada, estos procedimientos utilizan el tipo y la longitud de datos necesarios para representar todos los valores de los datos de la columna.  
  
 Cuando todos los valores de datos de una columna comparten el mismo tipo de datos, se utiliza ese tipo para toda la columna. Cuando los valores de datos de una columna utilizan tipos de datos diferentes, el tipo de datos de toda la columna se elige como se muestra a continuación.  
  
||INT|FLOAT|money|datetime|varchar|NVARCHAR|  
|------|---------|-----------|-----------|--------------|-------------|--------------|  
|**int**|**int**|**float**|**money**|**varchar**|**varchar**|**nvarchar**|  
|**float**|**float**|**float**|**money**|**varchar**|**varchar**|**nvarchar**|  
|**money**|**money**|**money**|**money**|**varchar**|**varchar**|**nvarchar**|  
|**datetime**|**varchar**|**varchar**|**varchar**|**datetime**|**varchar**|**nvarchar**|  
|**varchar**|**varchar**|**varchar**|**varchar**|**varchar**|**varchar**|**nvarchar**|  
|**nvarchar**|**nvarchar**|**nvarchar**|**nvarchar**|**nvarchar**|**nvarchar**|**nvarchar**|  
  
## <a name="remarks"></a>Comentarios  
 También puede usar **sp_OAMethod** para obtener un valor de propiedad.  
  
## <a name="permissions"></a>Permisos  
 Requiere la pertenencia al rol fijo de servidor **sysadmin** o al permiso Execute directamente en este procedimiento almacenado. la configuración de `Ole Automation Procedures` debe estar **habilitada** para utilizar cualquier procedimiento del sistema relacionado con la automatización OLE.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-calling-a-method"></a>A. Llamar a un método  
 En el ejemplo siguiente se llama al método `Connect` del objeto **SQLServer** creado previamente.  
  
```  
EXEC @hr = sp_OAMethod @object, 'Connect', NULL, 'my_server',  
    'my_login', 'my_password';  
IF @hr <> 0  
BEGIN  
   EXEC sp_OAGetErrorInfo @object  
    RETURN  
END;  
```  
  
### <a name="b-getting-a-property"></a>b. Obtener una propiedad  
 En el ejemplo siguiente se obtiene la propiedad `HostName` (del objeto **SQLServer** creado previamente) y se almacena en una variable local.  
  
```  
DECLARE @property varchar(255);  
EXEC @hr = sp_OAMethod @object, 'HostName', @property OUT;  
IF @hr <> 0  
BEGIN  
   EXEC sp_OAGetErrorInfo @object  
    RETURN  
END;  
PRINT @property;  
```  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos &#40;almacenados de automatización OLE de Transact&#41;-SQL](../../relational-databases/system-stored-procedures/ole-automation-stored-procedures-transact-sql.md)   
 [Ejemplo de script de automatización OLE](../../relational-databases/stored-procedures/ole-automation-sample-script.md)  
  
  
