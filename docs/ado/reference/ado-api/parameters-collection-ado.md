---
title: Colección de parámetros (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Command15::get_Parameters
- Command15::Parameters
- Command15::GetParameters
helpviewer_keywords:
- Parameters collection [ADO]
ms.assetid: 497cae10-3913-422a-9753-dcbb0a639b1b
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: a23b67141c7c07845438ed43f00d3124043a53c4
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2019
ms.locfileid: "66704118"
---
# <a name="parameters-collection-ado"></a>Colección de parámetros (ADO)
Contiene todos los [parámetro](../../../ado/reference/ado-api/parameter-object.md) objetos de un [comando](../../../ado/reference/ado-api/command-object-ado.md) objeto.  
  
## <a name="remarks"></a>Comentarios  
 Un **comando** objeto tiene un **parámetros** colección formada por **parámetro** objetos.  
  
 Mediante el [actualizar](../../../ado/reference/ado-api/refresh-method-ado.md) método en un **comando** del objeto **parámetros** colección recupera información de parámetros de proveedor para el procedimiento almacenado o una consulta parametrizada se especifica en el **comando** objeto. Algunos proveedores no admiten llamadas a procedimientos almacenados o consultas parametrizadas; una llamada a la **actualizar** método en el **parámetros** colección cuando se usa un proveedor de este tipo devolverá un error.  
  
 Si no ha definido su propia **parámetro** objetos y el acceso a la **parámetros** colección antes de llamar a la **actualizar** método, ADO llamará automáticamente a la método y rellenar la colección.  
  
 Puede minimizar las llamadas al proveedor para mejorar el rendimiento si conoce las propiedades de los parámetros asociados con el procedimiento almacenado o la consulta parametrizada que desea llamar. Usar el [CreateParameter](../../../ado/reference/ado-api/createparameter-method-ado.md) método para crear **parámetro** objetos con los valores de propiedad adecuados y el uso del [anexar](../../../ado/reference/ado-api/append-method-ado.md) método para agregarlos a la  **Parámetros** colección. Esto le permite establecer y devolver valores de parámetro sin tener que llamar al proveedor para obtener la información de parámetro. Si está escribiendo en un proveedor que no proporcione información de parámetros, debe rellenar manualmente el **parámetros** colección utilizando este método para que pueda usar en todos los parámetros. Use la [eliminar](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md) método para quitar **parámetro** objetos desde el **parámetros** colección si es necesario.  
  
 Los objetos en el **parámetros** colección de un **Recordset** vaya fuera del ámbito (por lo tanto, están disponibles) cuando el **Recordset** está cerrado.  
  
 Cuando se llama a un procedimiento almacenado con **comando**, el parámetro de valor devuelto y salida de un procedimiento almacenado se recupera como sigue:  
  
1.  Al llamar a un procedimiento almacenado que no tiene ningún parámetro, el **actualizar** método en el **parámetros** colección debe llamarse antes de llamar a la **Execute** método en el **Comando** objeto.  
  
2.  Cuando se llama a un procedimiento almacenado con parámetros y anexar explícitamente un parámetro a la **parámetros** colección con **Append**, el parámetro de valor devuelto y salida se debe anexar a la **Parámetros** colección. En primer lugar se debe anexar el valor devuelto a la **parámetros** colección. Use **Append** para agregar los demás parámetros en el **parámetros** colección en el orden de definición. Por ejemplo, el procedimiento almacenado SPWithParam tiene dos parámetros. El primer parámetro, *InParam*, es un parámetro de entrada que se definen como parámetros (20) y el segundo parámetro, *OutParam*, es un parámetro output definido como parámetros (20). Puede recuperar el parámetro de valor devuelto y salida con el código siguiente.  
  
    ```vb
    ' Open Connection Conn  
    set ccmd = CreateObject("ADODB.Command")  
    ccmd.Activeconnection= Conn  
  
    ccmd.CommandText="SPWithParam"  
    ccmd.commandType = 4 'adCmdStoredProc  
  
    ccmd.parameters.Append ccmd.CreateParameter(, adInteger, adParamReturnValue, , NULL)   ' return value  
    ccmd.parameters.Append ccmd.CreateParameter("InParam", adVarChar, adParamInput, 20, "hello world")   ' input parameter  
    ccmd.parameters.Append ccmd.CreateParameter("OutParam", adVarChar, adParamOutput, 20, NULL)   ' output parameter  
  
    ccmd.execute()  
  
    ' Access ccmd.parameters(0) as return value of this stored procedure  
    ' Access ccmd.parameters("OutParam") as the output parameter of this stored procedure.  
  
    ```  
  
3.  Cuando se llama a un procedimiento almacenado con parámetros y configuración de los parámetros mediante una llamada a la **elemento** método en el **parámetros** colección, el parámetro de valor devuelto y salida del procedimiento almacenado puede recuperarse de la **parámetros** colección. Por ejemplo, el procedimiento almacenado SPWithParam tiene dos parámetros. El primer parámetro, *InParam*, es un parámetro de entrada que se definen como parámetros (20) y el segundo parámetro, *OutParam*, es un parámetro output definido como parámetros (20). Puede recuperar el parámetro de valor devuelto y salida con el código siguiente.  
  
    ```vb
    ' Open Connection Conn  
    set ccmd = CreateObject("ADODB.Command")  
    ccmd.Activeconnection= Conn  
  
    ccmd.CommandText="SPWithParam"  
    ccmd.commandType = 4 'adCmdStoredProc  
  
    ccmd.parameters.Item("InParam").value = "hello world" ' input parameter  
    ccmd.execute()  
  
    ' Access ccmd.parameters(0) as return value of stored procedure  
    ' Access ccmd.parameters(2) or ccmd.parameters("OutParam") as the output parameter.  
    ```  
  
 Esta sección contiene el siguiente tema.  
  
-   [Los eventos, métodos y propiedades de la colección de parámetros](../../../ado/reference/ado-api/parameters-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vea también  
 [Append (método) (ADO)](../../../ado/reference/ado-api/append-method-ado.md)   
 [Método CreateParameter (ADO)](../../../ado/reference/ado-api/createparameter-method-ado.md)   
 [Objeto Parameter](../../../ado/reference/ado-api/parameter-object.md)
