---
title: Referencia de la interfaz de usuario del cuadro de diálogo Sugerir tipos de columna | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.suggestdatatypes.f1
ms.assetid: 8d5652e0-cf57-483f-828b-10f00c08418b
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: e2a1706a252ae9e70d214b4231442a201dfac88c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48058375"
---
# <a name="suggest-column-types-dialog-box-ui-reference"></a>Referencia de la interfaz de usuario del cuadro de diálogo Sugerir tipos de columna
  Utilice el cuadro de diálogo **Sugerir tipos de columna** para identificar el tipo de datos y la longitud de las columnas de un Administrador de conexiones de archivos planos basándose en un muestreo del contenido del archivo.  
  
 Para obtener más información sobre los tipos de datos que usa [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], vea [Tipos de datos de Integration Services](../data-flow/integration-services-data-types.md).  
  
## <a name="options"></a>Opciones  
 **Número de filas**  
 Escriba o seleccione el número de filas de la muestra que utiliza el algoritmo.  
  
 **Sugerir el tipo de datos entero más pequeño**  
 Desactive esta casilla para omitir la evaluación. Si está activada, determina el tipo de datos entero más pequeño posible en columnas que contienen datos numéricos integrales.  
  
 **Sugerir el tipo de datos real más pequeño**  
 Desactive esta casilla para omitir la evaluación. Si está activada, determina si las columnas que contienen datos numéricos reales pueden utilizar el tipo de datos real más pequeño, DT_R4.  
  
 **Identificar columnas booleanas mediante los valores siguientes**  
 Escriba los dos valores que desea utilizar como valores booleanos True y False. Los valores deben aparecer separados con una coma; el primer valor representa True.  
  
 **Rellenar columnas de cadena**  
 Active esta casilla para habilitar el relleno de cadenas.  
  
 **Porcentaje de relleno**  
 Escriba o seleccione el porcentaje de longitud de columna que se incrementará para tipos de datos de caracteres. El porcentaje debe ser un número entero.  
  
## <a name="see-also"></a>Vea también  
 [Referencia de mensajes y Error de Integration Services](../integration-services-error-and-message-reference.md)   
 [Administrador de conexiones de archivos planos](file-connection-manager.md)  
  
  
