---
title: Establecer análisis rápido | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: dcd1dc09-6eaf-440b-9ce6-fef779ff794f
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 7d41b15325586733ab54a37f4c3f007ce0253eaf
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66055818"
---
# <a name="set-fast-parse"></a>Configurar el análisis rápido
  La propiedad de análisis rápido debe configurarse para cada columna del origen o la transformación que utilice el análisis rápido. Para configurar la propiedad, utilice el Editor avanzado del origen de archivo plano y la transformación Conversión de datos.  
  
### <a name="to-set-fast-parse"></a>Para configurar el análisis rápido  
  
1.  Haga clic con el botón derecho en el origen de archivo plano o en la transformación Conversión de datos y, después, haga clic en **Mostrar editor avanzado**.  
  
2.  En el cuadro de diálogo **Editor avanzado** haga clic en la pestaña **Propiedades de entrada y salida** .  
  
3.  En el panel **Entradas y salidas** , haga clic en la columna para la cual desee habilitar el análisis rápido.  
  
4.  En el ventana Propiedades, expanda el nodo **propiedades personalizadas** y, a continuación `FastParse` , establezca `True`la propiedad en.  
  
5.  Haga clic en **OK**.  
  
  
