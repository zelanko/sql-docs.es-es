---
title: Configurar el análisis rápido | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
ms.assetid: dcd1dc09-6eaf-440b-9ce6-fef779ff794f
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 960876737e552e7c5a9af75cc23d7e43e3799735
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48170615"
---
# <a name="set-fast-parse"></a>Configurar el análisis rápido
  La propiedad de análisis rápido debe configurarse para cada columna del origen o la transformación que utilice el análisis rápido. Para configurar la propiedad, utilice el Editor avanzado del origen de archivo plano y la transformación Conversión de datos.  
  
### <a name="to-set-fast-parse"></a>Para configurar el análisis rápido  
  
1.  Haga clic con el botón derecho en el origen de archivo plano o en la transformación Conversión de datos y, después, haga clic en **Mostrar editor avanzado**.  
  
2.  En el cuadro de diálogo **Editor avanzado** haga clic en la pestaña **Propiedades de entrada y salida** .  
  
3.  En el panel **Entradas y salidas** , haga clic en la columna para la cual desee habilitar el análisis rápido.  
  
4.  En la ventana Propiedades, expanda el **propiedades personalizadas** nodo y, después, establezca el `FastParse` propiedad `True`.  
  
5.  Haga clic en **Aceptar**.  
  
  
