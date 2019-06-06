---
title: Usar ADO con Microsoft Visual Basic | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- ADO, Visual Basic
- Visual Basic [ADO]
ms.assetid: 9dfb6784-037d-4f9d-bb7f-b506b4498573
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: abbdbeec81a029716ac6516f9436373e91365a23
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2019
ms.locfileid: "66702778"
---
# <a name="using-ado-with-microsoft-visual-basic-and-visual-basic-for-applications"></a>Usar ADO con Microsoft Visual Basic y Visual Basic para aplicaciones
Cómo configurar un proyecto de ADO y escribir código de ADO son similar si usa Visual Basic o Visual Basic para aplicaciones. En este tema se aborda el uso de ADO con Visual Basic y Visual Basic para aplicaciones y destaca las diferencias.

## <a name="referencing-the-ado-library"></a>Hacer referencia a la biblioteca ADO
 El proyecto debe hacer referencia a la biblioteca ADO.

#### <a name="to-reference-ado-from-microsoft-visual-basic"></a>Para hacer referencia a ADO desde Microsoft Visual Basic

1.  En Visual Basic, desde el **proyecto** menú, seleccione **referencias...** .

2.  Seleccione **biblioteca Microsoft ActiveX Data Objects x.x** en la lista. Compruebe que al menos también se seleccionan las siguientes bibliotecas:

    -   Aplicaciones para Visual Studio

    -   Procedimientos y objetos en tiempo de ejecución de Visual Basic

    -   Procedimientos y objetos en Visual Basic

    -   OLE Automation

3.  Haga clic en **Aceptar**.

 Puede utilizar ADO fácilmente con Visual Basic para aplicaciones, mediante el uso de Microsoft Access, por ejemplo.

#### <a name="to-reference-ado-from-microsoft-access"></a>Para hacer referencia a ADO desde Microsoft Access

1.  En Microsoft Access, seleccione o cree un módulo desde la **módulos** pestaña en el **base de datos** ventana.

2.  En el **herramientas** menú, seleccione **referencias...** .

3.  Seleccione **biblioteca Microsoft ActiveX Data Objects x.x** en la lista. Compruebe que al menos también se seleccionan las siguientes bibliotecas:

    -   Aplicaciones para Visual Studio

    -   Biblioteca de objetos de Microsoft Access 8.0 (o posterior)

    -   Biblioteca de objetos de Microsoft DAO 3.5 (o posterior)

4.  Haga clic en **Aceptar**.

## <a name="creating-ado-objects-in-visual-basic"></a>Creación de objetos ADO en Visual Basic
 Para crear una variable de automation y una instancia de un objeto para esa variable, puede usar dos métodos: **Dim** o **CreateObject**.

### <a name="dim"></a>Dim
 Puede usar el **New** palabra clave with **Dim** para declarar y crear instancias de objetos ADO en un solo paso:

```
Dim conn As New ADODB.Connection
```

 Como alternativa, el **Dim** creación de instancias de declaración y el objeto de instrucción puede constar de dos pasos:

```
Dim conn As ADODB.Connection
Set conn = New ADODB.Connection
```

> [!NOTE]
>  No es necesario utilizar explícitamente la `ADODB` progid con el **Dim** instrucción, suponiendo que ha hecho referencia correctamente a la biblioteca ADO en el proyecto. Sin embargo, usarlo garantiza que no habrá conflictos de nomenclatura con otras bibliotecas.

> [!NOTE]
>  Por ejemplo, si se incluyen referencias a ADO y DAO en el mismo proyecto, debe incluir un calificador para especificar qué modelo de objetos para usar al crear instancias **Recordset** objetos, como se muestra en el código siguiente:

```
Dim adoRS As ADODB.Recordset
Dim daoRS As DAO.Recordset
```

### <a name="createobject"></a>CreateObject
 Con el **CreateObject** creación de instancias de método, la declaración y el objeto debe ser de dos pasos diferenciados:

```
Dim conn1
Set conn1 = CreateObject("ADODB.Connection") As Object
```

 Instancias de los objetos con **CreateObject** están enlazadas, lo que significa que no están fuertemente tipadas y finalización de la línea de comandos está deshabilitada. Sin embargo, le permiten omitir la referencia a la biblioteca ADO desde el proyecto y le permite crear instancias de versiones específicas de objetos. Por ejemplo:

```
Set conn1 = CreateObject("ADODB.Connection.2.0") As Object
```

 También podría hacerlo si específicamente crear una referencia a la biblioteca de tipos 2.0 de la versión de ADO y crear el objeto.

 Crear instancias de objetos mediante el uso de la **CreateObject** método es normalmente más lento que el uso de la **Dim** instrucción.

## <a name="handling-events"></a>Control de eventos
 Con el fin de controlar los eventos de ADO en Microsoft Visual Basic, debe declarar una variable nivel de módulo mediante la **WithEvents** palabra clave. La variable se puede declarar únicamente como parte de un módulo de clase y se debe declarar en el nivel de módulo. Para obtener una explicación más exhaustiva de control de eventos de ADO, vea [controlar eventos de ADO](../../../ado/guide/data/handling-ado-events.md).

## <a name="visual-basic-examples"></a>Ejemplos de Visual Basic
 Muchos ejemplos de Visual Basic se incluyen en la documentación de ADO. Para obtener más información, consulte [ejemplos de código ADO en Microsoft Visual Basic](../../../ado/reference/ado-api/ado-code-examples-in-visual-basic.md).

## <a name="see-also"></a>Vea también
 [Microsoft ActiveX Data Objects (ADO)](../../../ado/microsoft-activex-data-objects-ado.md) [usar ADO con Microsoft Visual C++](../../../ado/guide/appendixes/using-ado-with-microsoft-visual-c.md) [usar ADO con lenguajes de Scripting](../../../ado/guide/appendixes/using-ado-with-scripting-languages.md)
