---
description: Hacer referencia a las bibliotecas de ADO en una aplicación de Visual C++
title: Hacer referencia a las bibliotecas de ADO en una aplicación Visual C++ | Microsoft Docs
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- libraries [ADO]
- referencing libraries in a Visual C++ application[ADO]
- ADO, libraries
ms.assetid: d3ea12ec-bca8-48c3-af57-ce14576108c9
author: rothja
ms.author: jroth
ms.openlocfilehash: 7a262ef7b71b6618bdfc4ae50cec2eec3fca4a41
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2020
ms.locfileid: "88978486"
---
# <a name="referencing-the-ado-libraries-in-a-visual-c-application"></a>Hacer referencia a las bibliotecas de ADO en una aplicación de Visual C++
Para usar la versión más reciente de ADO en una aplicación Visual C++, utilice la siguiente `#import` Directiva:  
  
```cpp
#import "msado15.dll" \  
    no_namespace rename("EOF", "EndOfFile")  
```  
  
 Para usar ADO MD o ADOX, debe importar *msadomd.dll* o *msadox.dll*mediante la sintaxis anterior.  
  
## <a name="backward-compatibility"></a>Backward Compatibility  
 Para usar cualquier versión anterior de ADO, reemplace *msado15.dll* anterior por una de las siguientes bibliotecas de tipos.  
  
-   Biblioteca de tipos *msado27. tlb*, ADO 2,7  
  
-   Biblioteca de tipos *msado26. tlb*, ADO 2,6  
  
-   Biblioteca de tipos *msado25. tlb*, ADO 2,5  
  
-   Biblioteca de tipos *msado21. tlb*, ADO 2,1  
  
-   Biblioteca de tipos *msado20. tlb*, ADO 2,0
