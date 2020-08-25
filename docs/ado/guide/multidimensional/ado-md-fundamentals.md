---
description: Conceptos básicos de ADO MD
title: Aspectos básicos de ADO MD | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 02/15/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO MD, fundamentals
ms.assetid: f6a20d9f-c1ab-474c-b9f3-82277e2a126d
author: rothja
ms.author: jroth
ms.openlocfilehash: eb14a1b97ba6670b2170021bc354890b41fa01ca
ms.sourcegitcommit: c4d564435c008e2c92035efd2658172f20f07b2b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/24/2020
ms.locfileid: "88758795"
---
# <a name="ado-md-fundamentals"></a>Conceptos básicos de ADO MD
Los objetos de datos de Microsoft® ActiveX® (multidimensional) (ADO MD) proporcionan un acceso fácil a los datos multidimensionales de lenguajes como Microsoft Visual Basic® Microsoft Visual C++®. ADO MD extiende los objetos de datos (ADO) de Microsoft ActiveX® para incluir objetos específicos de datos multidimensionales, como los objetos [CubeDef](../../reference/ado-md-api/cubedef-object-ado-md.md) y [Cellset](../../reference/ado-md-api/cellset-object-ado-md.md) . Con ADO MD puede examinar esquemas multidimensionales, consultar un cubo y recuperar los resultados.  
  
 Como ADO, ADO MD usa un proveedor de OLE DB subyacente para obtener acceso a los datos. Para trabajar con ADO MD, el proveedor debe ser un proveedor de datos multidimensionales (MDP), tal y como se define en el OLE DB para la especificación de OLAP. Un MDP presenta datos en vistas multidimensionales en lugar de en vistas tabulares, que es el modo en que un proveedor de datos tabulares (TDP) presenta los datos. Consulte la documentación del proveedor de OLE DB OLAP para obtener más información sobre la sintaxis y el comportamiento específicos que admite el proveedor.  
  
 En este documento se supone un conocimiento práctico del lenguaje de programación de Visual Basic y un conocimiento general de ADO y OLAP. Para obtener más información, vea la [Guía del programador de ADO](../ado-programmer-s-guide.md) y [OLE DB para el procesamiento analítico en línea (OLAP)](/previous-versions/windows/desktop/ms717005(v=vs.85)).  
  
 Esta sección contiene los temas siguientes.  
  
-   [Información general de esquemas y datos multidimensionales](./overview-of-multidimensional-schemas-and-data.md)  
  
-   [Trabajo con datos multidimensionales](./working-with-multidimensional-data.md)  
  
-   [Uso de ADO con ADO MD](./using-ado-with-ado-md.md)  
  
-   [Programación con ADO MD](./programming-with-ado-md.md)  
  
## <a name="see-also"></a>Consulte también  
 [Modelo de objetos de ADO MD](../../reference/ado-md-api/ado-md-object-model.md)   
 [Guía del programador de ADO](../ado-programmer-s-guide.md)   
 [Extensiones de ADO para lenguaje de definición de datos y seguridad (ADOX)](../extensions/ado-extensions-for-data-definition-language-and-security-adox.md)   
 [Información general de los esquemas y datos multidimensionales](./overview-of-multidimensional-schemas-and-data.md)   
 [Programar con ADO MD](./programming-with-ado-md.md)   
 [Usar ADO con ADO MD](./using-ado-with-ado-md.md)   
 [Trabajo con datos multidimensionales](./working-with-multidimensional-data.md)