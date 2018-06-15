---
title: Hacer referencia a las bibliotecas de ADO en una aplicación de Visual C++ | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
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
ms.openlocfilehash: 6a38e5df65def060668e60ee470dc379b873ab35
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/11/2018
ms.locfileid: "35273614"
---
# <a name="referencing-the-ado-libraries-in-a-visual-c-application"></a>Hacer referencia a las bibliotecas de ADO en una aplicación de Visual C++
Para usar la versión más reciente de ADO en una aplicación de Visual C++, utilice la siguiente `#import` directiva:  
  
```  
#import "msado15.dll" \  
    no_namespace rename("EOF", "EndOfFile")  
```  
  
 Para usar ADO MD o ADOX, primero debe importar *msadomd.dll* o *msadox.dll*, utilizando la sintaxis anterior.  
  
## <a name="backward-compatibility"></a>Backward Compatibility  
 Para usar versiones anteriores de ADO, reemplace *msado15.dll* anteriormente con una de las siguientes bibliotecas de tipos.  
  
-   *msado27.tlb*, biblioteca de tipos 2.7 ADO  
  
-   *msado26.tlb*, biblioteca de tipos 2.6 ADO  
  
-   *msado25.tlb*, biblioteca de tipos 2,5 ADO  
  
-   *MSADO21*, biblioteca de tipos 2.1 ADO  
  
-   *msado20.tlb*, biblioteca de tipos 2.0 ADO
