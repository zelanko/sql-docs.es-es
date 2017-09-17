---
title: "Hacer referencia a las bibliotecas de ADO en una aplicación de Visual C++ | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.prod: sql-non-specified
ms.technology: "“drivers”"
ms.tgt_pltfrm: 
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
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 44d731d8c9e61c29f1dc9eb0c8ea12d57402639c
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

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
  
-   *msado27.tlb*, biblioteca de tipos 2.7 ADO  
  
-   *msado26.tlb*, biblioteca de tipos 2.6 ADO  
  
-   *msado25.tlb*, biblioteca de tipos 2,5 ADO  
  
-   *MSADO21*, biblioteca de tipos 2.1 ADO  
  
-   *msado20.tlb*, biblioteca de tipos 2.0 ADO
