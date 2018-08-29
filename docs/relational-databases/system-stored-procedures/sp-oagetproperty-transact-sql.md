---
title: sp_OAGetProperty (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_OAGetProperty_TSQL
- sp_OAGetProperty
dev_langs:
- TSQL
helpviewer_keywords:
- sp_OAGetProperty
ms.assetid: 240eeeb9-6d8b-4930-b912-1d273ca0ab38
caps.latest.revision: 27
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 348dd55dc3e2744c86b4b49b14a88fa95d186b6b
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2018
ms.locfileid: "43023034"
---
# <a name="spoagetproperty-transact-sql"></a>sp_OAGetProperty (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Obtiene el valor de una propiedad de un objeto OLE.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_OAGetProperty objecttoken , propertyname   
    [ , propertyvalue OUTPUT ]  
    [ , index...]   
```  
  
## <a name="arguments"></a>Argumentos  
 *objecttoken*  
 Es el token de un objeto OLE creado anteriormente mediante el uso de **sp_OACreate**.  
  
 *propertyname*  
 Es el nombre de la propiedad del objeto OLE que se devolverá.  
  
 *PropertyValue* **salida**  
 Es el valor devuelto de la propiedad. Si se especifica, debe ser una variable local del tipo de datos adecuado.  
  
 Si la propiedad devuelve un objeto OLE, *propertyvalue* debe ser una variable local del tipo de datos **int**. En la variable local se almacena un token de objeto que se puede utilizar con otros procedimientos almacenados de OLE Automation.  
  
 Si la propiedad devuelve un valor único, especifique una variable local para *propertyvalue*, que devuelve la propiedad de valor en la variable local; o no especifique *propertyvalue*, que devuelve el valor de propiedad al cliente como un conjunto de resultados de una sola columna, fila única.  
  
 Cuando la propiedad devuelve una matriz, si *propertyvalue* se especifica, se establece en NULL.  
  
 Si *propertyvalue* se especifica, pero la propiedad no devuelve un valor, se produce un error. Si la propiedad devuelve una matriz con más de dos dimensiones, se produce un error.  
  
 *index*  
 Es un parámetro de índice. Si se especifica, *índice* debe ser un valor de tipo de datos adecuado.  
  
 Algunas propiedades tienen parámetros. Estas propiedades se llaman propiedades indizadas y los parámetros se llaman parámetros de índice. Una propiedad puede tener varios parámetros de índice.  
  
> [!NOTE]  
>  Los parámetros para este procedimiento almacenado se especifican por posición, no por el nombre.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o un valor distinto de cero (error) que es el valor entero del HRESULT devuelto por el objeto de OLE Automation.  
  
 Para obtener más información sobre los códigos de retorno HRESULT, vea [OLE Automation códigos de retorno e información de Error](../../relational-databases/stored-procedures/ole-automation-return-codes-and-error-information.md).  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Si la propiedad devuelve una matriz con una o dos dimensiones, la matriz se devuelve al cliente como un conjunto de resultados:  
  
-   Se devuelve al cliente una matriz unidimensional como conjunto de resultados de fila única con tantas columnas como elementos tenga la matriz. En otras palabras, la matriz se devuelve como columnas.  
  
-   Se devuelve al cliente una matriz bidimensional como conjunto de resultados con tantas columnas como elementos haya en la primera dimensión de la matriz y con tantas filas como elementos haya en la segunda dimensión de la matriz. En otras palabras, la matriz se devuelve como (columnas, filas).  
  
 Cuando el valor devuelto de una propiedad o valor devuelto de método es una matriz, **sp_OAGetProperty** o **sp_OAMethod** devuelve un conjunto de resultados para el cliente. (Los parámetros de salida del método no pueden ser matrices.) Estos procedimientos recorren todos los valores de datos de la matriz para determinar los tipos de datos y las longitudes de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] adecuados para cada columna del conjunto de resultados. Para una columna determinada, estos procedimientos utilizan el tipo y la longitud de datos necesarios para representar todos los valores de los datos de la columna.  
  
 Cuando todos los valores de datos de una columna comparten el mismo tipo de datos, se utiliza ese tipo para toda la columna. Cuando los valores de datos de una columna utilizan tipos de datos diferentes, el tipo de datos de toda la columna se elige como se muestra a continuación.  
  
||INT|FLOAT|money|DATETIME|varchar|NVARCHAR|  
|------|---------|-----------|-----------|--------------|-------------|--------------|  
|**int**|**int**|**float**|**money**|**varchar**|**varchar**|**nvarchar**|  
|**float**|**float**|**float**|**money**|**varchar**|**varchar**|**nvarchar**|  
|**money**|**money**|**money**|**money**|**varchar**|**varchar**|**nvarchar**|  
|**datetime**|**varchar**|**varchar**|**varchar**|**datetime**|**varchar**|**nvarchar**|  
|**varchar**|**varchar**|**varchar**|**varchar**|**varchar**|**varchar**|**nvarchar**|  
|**nvarchar**|**nvarchar**|**nvarchar**|**nvarchar**|**nvarchar**|**nvarchar**|**nvarchar**|  
  
## <a name="remarks"></a>Notas  
 También puede usar **sp_OAMethod** para obtener un valor de propiedad.  
  
## <a name="permissions"></a>Permisos  
 Requiere la pertenencia al rol fijo de servidor **sysadmin** .  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-using-a-local-variable"></a>A. Usar una variable local  
 En el ejemplo siguiente se obtiene el `HostName` propiedad (de creado previamente **SQLServer** objeto) y lo almacena en una variable local.  
  
```  
DECLARE @property varchar(255);  
EXEC @hr = sp_OAGetProperty @object, 'HostName', @property OUT;  
IF @hr <> 0  
BEGIN  
   EXEC sp_OAGetErrorInfo @object  
    RETURN  
END  
PRINT @property;  
```  
  
### <a name="b-using-a-result-set"></a>B. Usar un conjunto de resultados  
 En el ejemplo siguiente se obtiene el `HostName` propiedad (de creado previamente **SQLServer** objeto) y devuelve al cliente como un conjunto de resultados.  
  
```  
EXEC @hr = sp_OAGetProperty @object, 'HostName';  
IF @hr <> 0  
BEGIN  
   EXEC sp_OAGetErrorInfo @object  
    RETURN  
END;  
```  
  
## <a name="see-also"></a>Vea también  
 [OLE Automation procedimientos almacenados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/ole-automation-stored-procedures-transact-sql.md)   
 [Ejemplo de script de automatización OLE](../../relational-databases/stored-procedures/ole-automation-sample-script.md)  
  
  
