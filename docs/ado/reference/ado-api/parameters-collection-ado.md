---
title: "Colección de parámetros (ADO) | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Command15::get_Parameters
- Command15::Parameters
- Command15::GetParameters
helpviewer_keywords:
- Parameters collection [ADO]
ms.assetid: 497cae10-3913-422a-9753-dcbb0a639b1b
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9dcfec51eb94eb1ca290ebb3323012e2aaa558b5
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="parameters-collection-ado"></a>Colección de parámetros (ADO)
Contiene todos los [parámetro](../../../ado/reference/ado-api/parameter-object.md) objetos de un [comando](../../../ado/reference/ado-api/command-object-ado.md) objeto.  
  
## <a name="remarks"></a>Comentarios  
 A **comando** objeto tiene una **parámetros** colección formada por **parámetro** objetos.  
  
 Mediante el [actualizar](../../../ado/reference/ado-api/refresh-method-ado.md) método en un **comando** del objeto **parámetros** colección recupera información de parámetros de proveedor para el procedimiento almacenado o la consulta parametrizada se especifica en el **comando** objeto. Algunos proveedores no admiten llamadas a procedimientos almacenados o consultas parametrizadas; llamar a la **actualizar** método en el **parámetros** colección cuando se usa este tipo de proveedor, devolverá un error.  
  
 Si no ha definido su propia **parámetro** objetos y el acceso a la **parámetros** colección antes de llamar a la **actualizar** método, ADO llama automáticamente a la método y rellenar la colección.  
  
 Puede minimizar llamadas al proveedor para mejorar el rendimiento si conoce las propiedades de los parámetros asociados con el procedimiento almacenado o la consulta parametrizada que se va a llamar. Utilice la [CreateParameter](../../../ado/reference/ado-api/createparameter-method-ado.md) método para crear **parámetro** objetos con los valores de propiedad adecuados y utilice el [anexado](../../../ado/reference/ado-api/append-method-ado.md) método para agregarlos a la ** Parámetros de** colección. Esto permite establecer y devolver valores de parámetro sin tener que llamar al proveedor para obtener la información de parámetro. Si está escribiendo en un proveedor que no proporcione información de parámetros, debe rellenar manualmente la **parámetros** colección con este método para que pueda usar en todos los parámetros. Use la [eliminar](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md) método para quitar **parámetro** objetos desde la **parámetros** colección si es necesario.  
  
 Los objetos de la **parámetros** colección de un **Recordset** vaya fuera del ámbito (y, por tanto, no están disponibles) cuando el **Recordset** está cerrado.  
  
 Cuando se llama a un procedimiento almacenado con **comando**, el parámetro de salida o valor devuelto de un procedimiento almacenado se recupera como sigue:  
  
1.  Al llamar a un procedimiento almacenado que no tiene ningún parámetro, el **actualizar** método en el **parámetros** colección debe llamarse antes de llamar a la **Execute** método en el **Comando** objeto.  
  
2.  Cuando se llama a un procedimiento almacenado con parámetros y anexar explícitamente un parámetro a la **parámetros** colección con **anexado**, el parámetro de salida o valor devuelto se debe anexar a la **Parámetros** colección. El valor devuelto en primer lugar debe agregarse a la **parámetros** colección. Use **anexado** para agregar los otros parámetros en la **parámetros** colección en el orden de definición. Por ejemplo, el procedimiento almacenado SPWithParam tiene dos parámetros. El primer parámetro, *InParam*, es un parámetro de entrada definido como parámetros (20) y el segundo parámetro, *OutParam*, es un parámetro output definido como parámetros (20). Puede recuperar el parámetro de salida o valor devuelto por el código siguiente.  
  
    ```  
    ' Open Connection Conn  
    set ccmd = CreateObject("ADODB.Command")  
    ccmd.Activeconnection= Conn  
  
    ccmd.CommandText="SPWithParam"  
    ccmd.commandType = 4 'adCmdStoredProc  
  
    ccmd.parameters.Append ccmd.CreateParameter(, adInteger, adParamReturnValue, , NULL)   ' return value  
    ccmd.parameters.Append ccmd.CreateParameter("InParam", adVarChar, adParamInput, 20, "hello world")   ' input parameter  
    ccmd.parameters.Append ccmd.CreateParameter("OutParam", adVarChar, adParamOuput, 20, NULL)   ' output parameter  
  
    ccmd.execute()  
  
    ' Access ccmd.parameters(0) as return value of this stored procedure  
    ' Access ccmd.parameters("OutParam") as the output parameter of this stored procedure.  
  
    ```  
  
3.  Cuando se llama a un procedimiento almacenado con parámetros y la configuración de los parámetros mediante una llamada a la **elemento** método en el **parámetros** recopilación, el parámetro de salida o valor devuelto del procedimiento almacenado puede recuperar desde el **parámetros** colección. Por ejemplo, el procedimiento almacenado SPWithParam tiene dos parámetros. El primer parámetro, *InParam*, es un parámetro de entrada definido como parámetros (20) y el segundo parámetro, *OutParam*, es un parámetro output definido como parámetros (20). Puede recuperar el parámetro de salida o valor devuelto por el código siguiente.  
  
    ```  
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
  
-   [Eventos, métodos y propiedades de la colección de parámetros](../../../ado/reference/ado-api/parameters-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vea también  
 [Append (método) (ADO)](../../../ado/reference/ado-api/append-method-ado.md)   
 [Método CreateParameter (ADO)](../../../ado/reference/ado-api/createparameter-method-ado.md)   
 [Objeto de parámetro](../../../ado/reference/ado-api/parameter-object.md)
