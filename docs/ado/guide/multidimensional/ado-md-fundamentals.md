---
title: Conceptos básicos de ADO MD | Documentos de Microsoft
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 02/15/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO MD, fundamentals
ms.assetid: f6a20d9f-c1ab-474c-b9f3-82277e2a126d
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5d15a76c1a7109c6c08d95610278ba4ac9d5c37a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="ado-md-fundamentals"></a>Conceptos básicos de ADO MD
Microsoft® ActiveX® Data Objects (Multidimensional) (ADO MD) proporciona un acceso sencillo a datos multidimensionales de lenguajes como Microsoft Visual Basic®, Microsoft Visual C++®. ADO MD amplía Microsoft ActiveX® Data Objects (ADO) para incluir objetos específicos de datos multidimensionales, como el [CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md) y [Cellset](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) objetos. Con ADO MD puede explorar un esquema multidimensional, consultar un cubo y recuperar los resultados.  
  
 Al igual que ADO, ADO MD utiliza un proveedor OLE DB subyacente para obtener acceso a datos. Para trabajar con ADO MD, el proveedor debe ser un proveedor de datos multidimensionales (MDP) de acuerdo con la especificación OLE DB para OLAP. Un MDP presenta los datos en vistas multidimensionales, en lugar de vistas tabulares, que es la manera en que un proveedor de datos tabulares (TDP) presenta los datos. Consulte la documentación para el proveedor OLE DB de OLAP para obtener más información sobre la sintaxis específica y el comportamiento compatible con el proveedor.  
  
 Este documento asume un conocimiento práctico del lenguaje de programación de Visual Basic y conocimientos generales de ADO y OLAP. Para obtener más información, consulte el [Guía del programador de ADO](../../../ado/guide/ado-programmer-s-guide.md) y [OLE DB para OLAP Online Analytical Processing ()](https://msdn.microsoft.com/library/windows/desktop/ms717005.aspx).  
  
 Esta sección contiene los temas siguientes.  
  
-   [Información general de esquemas y datos multidimensionales](../../../ado/guide/multidimensional/overview-of-multidimensional-schemas-and-data.md)  
  
-   [Trabajo con datos multidimensionales](../../../ado/guide/multidimensional/working-with-multidimensional-data.md)  
  
-   [Uso de ADO con ADO MD](../../../ado/guide/multidimensional/using-ado-with-ado-md.md)  
  
-   [Programación con ADO MD](../../../ado/guide/multidimensional/programming-with-ado-md.md)  
  
## <a name="see-also"></a>Vea también  
 [Modelo de objetos de ADO MD](../../../ado/reference/ado-md-api/ado-md-object-model.md)   
 [Guía del programador de ADO](../../../ado/guide/ado-programmer-s-guide.md)   
 [Extensiones de ADO para lenguaje de definición de datos y seguridad (ADOX)](../../../ado/guide/extensions/ado-extensions-for-data-definition-language-and-security-adox.md)   
 [Información general de esquemas y datos multidimensionales](../../../ado/guide/multidimensional/overview-of-multidimensional-schemas-and-data.md)   
 [Programar con ADO MD](../../../ado/guide/multidimensional/programming-with-ado-md.md)   
 [Usar ADO con ADO MD](../../../ado/guide/multidimensional/using-ado-with-ado-md.md)   
 [Trabajo con datos multidimensionales](../../../ado/guide/multidimensional/working-with-multidimensional-data.md)
