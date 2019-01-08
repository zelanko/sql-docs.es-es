---
title: Opciones de atributos fijos y variables (Asistente para dimensiones de variación lenta) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.loaddimwizard.attriboption.f1
ms.assetid: c841345c-7d03-452f-9379-1c8c464f029c
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 1edcb27ac2be97919fb3d494b35afc1fab25c204
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52756747"
---
# <a name="fixed-and-changing-attribute-options-slowly-changing-dimension-wizard"></a>Opciones de atributos fijos y variables (Asistente para dimensiones variables)
  Utilice el cuadro de diálogo **Opciones de atributos fijos y variables** para especificar cómo se debe responder a los cambios realizados en los atributos fijos y variables.  
  
 Para obtener más información acerca de este asistente, vea [Slowly Changing Dimension Transformation](slowly-changing-dimension-transformation.md).  
  
## <a name="options"></a>Opciones  
 **Atributos fijos**  
 En el caso de los atributos fijos, indique si la tarea debe dar un error cuando se detecte un cambio en un atributo fijo.  
  
 **Atributos variables**  
 En el caso de los atributos variables, indique si la tarea debe cambiar todos los registros no actualizados o expirados, además de los actuales, cuando se detecten cambios en un atributo variable. Los registros expirados son los que se han reemplazado por uno nuevo mediante un cambio en un atributo histórico (un cambio del Tipo 2). La selección de esta opción puede imponer requisitos adicionales de procesamiento en un objeto multidimensional generado en el almacenamiento de datos relacional.  
  
## <a name="see-also"></a>Vea también  
 [Configurar salidas mediante el Asistente para dimensión de variación lenta](configure-outputs-using-the-slowly-changing-dimension-wizard.md)  
  
  
