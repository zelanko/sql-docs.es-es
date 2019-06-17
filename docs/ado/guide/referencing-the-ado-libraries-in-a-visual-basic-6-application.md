---
title: Hacer referencia a las bibliotecas de ADO en una aplicación Visual Basic 6 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- libraries [ADO]
- referencing libraries in a Visual Basic application[ADO]
- ADO, libraries
ms.assetid: cfd37a82-aad2-41cd-8d13-1566c43d95f0
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 80385161bcfce2c4b39ec9fa1257358cabe5f98c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66704379"
---
# <a name="referencing-the-ado-libraries-in-a-visual-basic-6-application"></a>Hacer referencia a las bibliotecas de ADO en una aplicación de Visual Basic 6
Para importar las bibliotecas de ADO en una aplicación de Microsoft Visual Basic 6, debe establecer una referencia en el proyecto de Visual Basic.  
  
### <a name="to-set-a-reference-to-the-ado-libraries-in-a-visual-basic-project"></a>Para establecer una referencia a las bibliotecas de ADO en un proyecto de Visual Basic  
  
1.  Cree un nuevo o abra un proyecto existente de Visual Basic.  
  
2.  Haga clic en el **proyecto** elemento de menú y, a continuación, seleccione **referencias...**  desde el panel de menú desplegable.  
  
3.  Desde **referencias disponibles**, active la casilla de **Microsoft ActiveX Data Objects *Observe* biblioteca**, donde ***Observe*** representa la versión más reciente número de versión. El **ubicación** campo siguiente debe identificar su elección como *$installDir\msado15.dll*, donde *$installDir* representa la ruta de acceso del directorio en el que la biblioteca ADO se ha instalado.  
  
4.  Si piensa utilizar ADO MD, repita el paso 3 para seleccionar **Microsoft ActiveX Data Objects (multidimensional) *Observe* biblioteca**. El **ubicación** campo debería identificar esta opción como *$installDir\msadomd.dll*.  
  
5.  Si piensa usar ADOX, repita el paso 3 para seleccionar **Microsoft ADO Ext. *Observe* de DDL y seguridad**. El **ubicación** campo debería identificar esta opción como *$installDir\msadox.dll*.  
  
6.  Haga clic en **Aceptar** para terminar de configurar las referencias.  
  
## <a name="backward-compatibility"></a>Backward Compatibility  
 Instalación de ADO, también copia las bibliotecas de tipos siguientes de las versiones anteriores:  
  
-   *msado27.tlb*, biblioteca de tipos de 2,7 ADO  
  
-   *msado26.tlb*, biblioteca de tipos de 2,6 ADO  
  
-   *msado25.tlb*, biblioteca de tipos de 2,5 ADO  
  
-   *MSADO21*, biblioteca de tipos 2.1 de ADO  
  
-   *msado20.tlb*, biblioteca de tipos 2.0 ADO  
  
 Si la aplicación debe utilizar ninguna de estas bibliotecas de ADO por motivos de compatibilidad con versiones anteriores, deberá importar la versión adecuada de la biblioteca de tipos. Para ello, siga los procedimientos descritos en la sección anterior, reemplazando *msado15.dll* por *msadoXX.tlb*, donde *XX* representa el número de versión que necesite para importar.
