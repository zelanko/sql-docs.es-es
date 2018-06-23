---
title: Configurar el análisis rápido | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: dcd1dc09-6eaf-440b-9ce6-fef779ff794f
caps.latest.revision: 5
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 94f4fe123cb37e60e175ad39b932e61376e217b8
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36106144"
---
# <a name="set-fast-parse"></a>Configurar el análisis rápido
  La propiedad de análisis rápido debe configurarse para cada columna del origen o la transformación que utilice el análisis rápido. Para configurar la propiedad, utilice el Editor avanzado del origen de archivo plano y la transformación Conversión de datos.  
  
### <a name="to-set-fast-parse"></a>Para configurar el análisis rápido  
  
1.  Haga clic con el botón derecho en el origen de archivo plano o en la transformación Conversión de datos y, después, haga clic en **Mostrar editor avanzado**.  
  
2.  En el cuadro de diálogo **Editor avanzado** haga clic en la pestaña **Propiedades de entrada y salida** .  
  
3.  En el panel **Entradas y salidas** , haga clic en la columna para la cual desee habilitar el análisis rápido.  
  
4.  En la ventana Propiedades, expanda el **propiedades personalizadas** nodo y, después, establezca el `FastParse` propiedad `True`.  
  
5.  Haga clic en **Aceptar**.  
  
  