---
title: Hacer referencia a las bibliotecas de ADO en una aplicación de Visual Basic 6 | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- libraries [ADO]
- referencing libraries in a Visual Basic application[ADO]
- ADO, libraries
ms.assetid: cfd37a82-aad2-41cd-8d13-1566c43d95f0
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d2c2aa317f9d4ff810cba13fbb315ce090997583
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="referencing-the-ado-libraries-in-a-visual-basic-6-application"></a>Hacer referencia a las bibliotecas de ADO en una aplicación de Visual Basic 6
Para importar las bibliotecas de ADO en una aplicación de Microsoft Visual Basic 6, debe establecer una referencia en el proyecto de Visual Basic.  
  
### <a name="to-set-a-reference-to-the-ado-libraries-in-a-visual-basic-project"></a>Para establecer una referencia a las bibliotecas de ADO en un proyecto de Visual Basic  
  
1.  Cree un nuevo o abra un proyecto existente de Visual Basic.  
  
2.  Haga clic en el **proyecto** elemento de menú y, a continuación, seleccione **referencias...**  desde el panel de menú desplegable.  
  
3.  De **referencias disponibles**, active la casilla de **Microsoft ActiveX Data Objects *Observe* biblioteca**, donde ***Observe*** representa la versión más reciente número de versión. El **ubicación** campo siguiente debería identificar su elección como *$installDir\msado15.dll*, donde *$installDir* representa la ruta de acceso del directorio en el que la biblioteca de ADO se ha instalado.  
  
4.  Si piensa usar ADO MD, repita el paso 3 para seleccionar **Microsoft ActiveX Data Objects (multidimensional) *Observe* biblioteca**. El **ubicación** campo debería identificar esta opción como *$installDir\msadomd.dll*.  
  
5.  Si piensa usar ADOX, repita el paso 3 para seleccionar **Microsoft ADO Ext. *Observe* de DDL y seguridad**. El **ubicación** campo debería identificar esta opción como *$installDir\msadox.dll*.  
  
6.  Haga clic en **Aceptar** para terminar de configurar las referencias.  
  
## <a name="backward-compatibility"></a>Compatibilidad con versiones anteriores  
 Instalar ADO, también copia las bibliotecas de tipos siguientes de versiones anteriores:  
  
-   *msado27.tlb*, biblioteca de tipos 2.7 ADO  
  
-   *msado26.tlb*, biblioteca de tipos 2.6 ADO  
  
-   *msado25.tlb*, biblioteca de tipos 2,5 ADO  
  
-   *MSADO21*, biblioteca de tipos 2.1 ADO  
  
-   *msado20.tlb*, biblioteca de tipos 2.0 ADO  
  
 Si la aplicación debe utilizar cualquiera de estas bibliotecas de ADO por motivos de compatibilidad con versiones anteriores, debe importar la versión adecuada de la biblioteca de tipos. Para ello, siga los procedimientos descritos en la sección anterior, reemplazando *msado15.dll* por *msadoXX.tlb*, donde *XX* representa el número de versión que se debe importar.
