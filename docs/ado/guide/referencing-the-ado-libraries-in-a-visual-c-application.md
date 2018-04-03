---
title: Hacer referencia a las bibliotecas de ADO en una aplicación de Visual C++ | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology: drivers
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- C++
helpviewer_keywords:
- libraries [ADO]
- referencing libraries in a Visual C++ application[ADO]
- ADO, libraries
ms.assetid: d3ea12ec-bca8-48c3-af57-ce14576108c9
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d5cbc06a7ddf9452a96d2a3edff30b941a8d5f2b
ms.sourcegitcommit: 8f1d1363e18e0c32ff250617ab6cb2da2147bf8e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/03/2018
---
# <a name="referencing-the-ado-libraries-in-a-visual-c-application"></a>Hacer referencia a las bibliotecas de ADO en una aplicación de Visual C++
Para usar la versión más reciente de ADO en una aplicación de Visual C++, utilice la siguiente `#import` directiva:  
  
```  
#import "msado15.dll" \  
    no_namespace rename("EOF", "EndOfFile")  
```  
  
 Para usar ADO MD o ADOX, primero debe importar *msadomd.dll* o *msadox.dll*, utilizando la sintaxis anterior.  
  
## <a name="backward-compatibility"></a>Compatibilidad con versiones anteriores  
 Para usar versiones anteriores de ADO, reemplace *msado15.dll* anteriormente con una de las siguientes bibliotecas de tipos.  
  
-   *msado27.tlb*, ADO 2.7 Type Library  
  
-   *msado26.tlb*, biblioteca de tipos 2.6 ADO  
  
-   *msado25.tlb*, ADO 2.5 Type Library  
  
-   *msado21.tlb*, ADO 2.1 Type Library  
  
-   *msado20.tlb*, ADO 2.0 Type Library
