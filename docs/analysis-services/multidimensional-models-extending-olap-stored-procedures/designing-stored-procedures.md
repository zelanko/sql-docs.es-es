---
title: "Diseñar procedimientos almacenados | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- stored procedures [Analysis Services], designing
- dependent assemblies [Analysis Services]
- assemblies [Analysis Services]
ms.assetid: af4e7bd5-041b-4a40-9942-0ef6a3af46c6
caps.latest.revision: 28
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7ce4810cec6ebfe861150aa24fea322682dc0e8c
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="designing-stored-procedures"></a>Diseñar procedimientos almacenados
  El modelo de objeto administrativo Objetos de administración de análisis (AMO) y el modelo de objeto orientado al cliente Objetos de datos [!INCLUDE[msCoName](../../includes/msconame-md.md)] ActiveX® (Multidimensional) (ADO MD) se incluyen en los procedimientos almacenados.  
  
 Los procedimientos almacenados deben estar en el ámbito (el servidor o la base de datos) para ser visibles en el nivel de Expresiones multidimensionales (MDX) para ser llamados. Sin embargo, cuando se invoca un procedimiento almacenado, su ámbito no se limita a acciones bajo su elemento primario. Un procedimiento almacenado puede realizar cambios o modificaciones en cualquier lugar del servidor, sujeto únicamente a las limitaciones de seguridad del proceso de usuario que lo invoca o a las limitaciones de la transacción en la que opera.  
  
 Los procedimientos del ámbito del servidor están disponibles en todos los contextos del servidor. Los procedimientos almacenados del ámbito de la base de datos solamente están visibles en el contexto de la base de datos en la que se definen.  
  
 Al igual que con cualquier función MDX, para que pueda continuar una sesión MDX se debe resolver el procedimiento almacenado; los procedimientos almacenados bloquean las sesiones MDX mientras se ejecutan. A menos que exista una razón específica para detener una sesión MDX pendiente de interacción del usuario, se desaconsejan las interacciones del usuario (como los cuadros de diálogo).  
  
## <a name="dependent-assemblies"></a>Ensamblados dependientes  
 Todos los ensamblados dependientes se deben cargar en una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para que los encuentre Common Language Runtime (CLR). [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] almacena los ensamblados dependientes en la misma carpeta que el ensamblado principal, de manera que CLR resuelve automáticamente todas las referencias de función a las funciones en esos ensamblados.  
  
## <a name="see-also"></a>Vea también  
 [Administración de ensamblados de modelos multidimensionales](../../analysis-services/multidimensional-models/multidimensional-model-assemblies-management.md)   
 [Definir procedimientos almacenados](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/defining-stored-procedures.md)  
  
  
