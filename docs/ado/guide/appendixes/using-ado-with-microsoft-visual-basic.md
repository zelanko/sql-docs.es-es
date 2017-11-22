---
title: Usar ADO con Microsoft Visual Basic | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: VB
helpviewer_keywords:
- ADO, Visual Basic
- Visual Basic [ADO]
ms.assetid: 9dfb6784-037d-4f9d-bb7f-b506b4498573
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: ef8260be592439a3130afe9af830b8159290f2a2
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="using-ado-with-microsoft-visual-basic-and-visual-basic-for-applications"></a>Usar ADO con Microsoft Visual Basic y Visual Basic para aplicaciones
Cómo configurar un proyecto de ADO y escribir código de ADO son similar si utiliza Visual Basic o Visual Basic para aplicaciones. Este tema aborda el uso de ADO con Visual Basic y Visual Basic para aplicaciones y destaca las diferencias.

## <a name="referencing-the-ado-library"></a>Hacer referencia a la biblioteca de ADO
 El proyecto debe hacer referencia a la biblioteca de ADO.

#### <a name="to-reference-ado-from-microsoft-visual-basic"></a>Para hacer referencia a ADO desde Microsoft Visual Basic

1.  En Visual Basic, desde el **proyecto** menú, seleccione **referencias...** .

2.  Seleccione **biblioteca Microsoft ActiveX Data Objects x.x** en la lista. Compruebe que al menos también se seleccionan las bibliotecas siguientes:

    -   Aplicaciones para Visual Studio

    -   Los procedimientos y objetos en tiempo de ejecución de Visual Basic

    -   Los procedimientos y objetos en Visual Basic

    -   OLE Automation

3.  Haga clic en **Aceptar**.

 Se puede utilizar ADO igual de sencillo con Visual Basic para aplicaciones, mediante el uso de Microsoft Access, por ejemplo.

#### <a name="to-reference-ado-from-microsoft-access"></a>Para hacer referencia a ADO desde Microsoft Access

1.  En Microsoft Access, seleccione o cree un módulo desde la **módulos** pestaña en el **base de datos** ventana.

2.  En el **herramientas** menú, seleccione **referencias...** .

3.  Seleccione **biblioteca Microsoft ActiveX Data Objects x.x** en la lista. Compruebe que al menos también se seleccionan las bibliotecas siguientes:

    -   Aplicaciones para Visual Studio

    -   Biblioteca de objetos de Microsoft Access 8.0 (o posterior)

    -   Biblioteca de objetos de Microsoft DAO 3.5 (o posterior)

4.  Haga clic en **Aceptar**.

## <a name="creating-ado-objects-in-visual-basic"></a>Crear objetos de ADO en Visual Basic
 Para crear una variable de automatización y una instancia de un objeto para esa variable, puede utilizar dos métodos: **Dim** o **CreateObject**.

### <a name="dim"></a>Dim
 Puede usar el **New** palabra clave with **Dim** para declarar y crear instancias de objetos de ADO en un solo paso:

```
Dim conn As New ADODB.Connection
```

 Como alternativa, el **Dim** creación de instancias de declaración y el objeto de instrucción puede constar de dos pasos:

```
Dim conn As ADODB.Connection
Set conn = New ADODB.Connection
```

> [!NOTE]
>  No es necesario utilizar explícitamente la `ADODB` progid con el **Dim** instrucción, suponiendo que ha hecho referencia correctamente a la biblioteca de ADO en el proyecto. Sin embargo, usarlo garantiza que no tenga conflictos de nomenclatura con otras bibliotecas.

> [!NOTE]
>  Por ejemplo, si se incluyen referencias a ADO y DAO en el mismo proyecto, se debe incluir un calificador para especificar el modelo de objeto que se usará al crear instancias de **Recordset** objetos, como en el código siguiente:

```
Dim adoRS As ADODB.Recordset
Dim daoRS As DAO.Recordset
```

### <a name="createobject"></a>CreateObject
 Con el **CreateObject** creación de instancias de método, la declaración y el objeto debe constar de dos pasos discretos:

```
Dim conn1
Set conn1 = CreateObject("ADODB.Connection") As Object
```

 Instancias de los objetos con **CreateObject** son en tiempo de ejecución, lo que significa que no están fuertemente tipadas y la finalización de línea de comandos está deshabilitada. Sin embargo, ¿le permite omitir la referencia a la biblioteca de ADO desde el proyecto y le permite crear instancias de versiones específicas de objetos. Por ejemplo:

```
Set conn1 = CreateObject("ADODB.Connection.2.0") As Object
```

 También puede hacerlo si crear específicamente una referencia a la biblioteca de tipos 2.0 de la versión de ADO y crear el objeto.

 Crear instancias de objetos mediante el uso de la **CreateObject** método es normalmente más lento que usar la **Dim** instrucción.

## <a name="handling-events"></a>Control de eventos
 Para controlar eventos de ADO en Microsoft Visual Basic, debe declarar una variable de nivel de módulo utilizando el **WithEvents** palabra clave. La variable se puede declarar únicamente como parte de un módulo de clase y se debe declarar en el nivel de módulo. Para obtener una explicación más exhaustiva de control de eventos de ADO, vea [controlar eventos de ADO](../../../ado/guide/data/handling-ado-events.md).

## <a name="visual-basic-examples"></a>Ejemplos de Visual Basic
 Muchos ejemplos de Visual Basic se incluyen en la documentación de ADO. Para obtener más información, consulte [ejemplos de código ADO en Microsoft Visual Basic](../../../ado/reference/ado-api/ado-code-examples-in-visual-basic.md).

## <a name="see-also"></a>Vea también
 [Microsoft ActiveX Data Objects (ADO)](../../../ado/microsoft-activex-data-objects-ado.md) [usar ADO con Microsoft Visual C++](../../../ado/guide/appendixes/using-ado-with-microsoft-visual-c.md) [usar ADO con lenguajes de Scripting](../../../ado/guide/appendixes/using-ado-with-scripting-languages.md)
