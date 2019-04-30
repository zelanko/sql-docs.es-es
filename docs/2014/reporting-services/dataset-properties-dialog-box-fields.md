---
title: Cuadro de diálogo de propiedades de conjunto de datos, campos | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.datasetproperties.fields.f1
- "10140"
ms.assetid: e1367556-736e-4a6b-b9e7-10432a3e50b5
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 3b1c49beb22a3a91e3d42aa7ce4ed99b5e107b4d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63164970"
---
# <a name="dataset-properties-dialog-box-fields"></a>Propiedades del conjunto de datos (cuadro de diálogo), Campos
  Seleccione **Campos** en el cuadro de diálogo **Propiedades del conjunto de datos** para cambiar la colección de campos para el conjunto de datos del informe. La lista de campos se rellena automáticamente, pero puede utilizar **Campos** para agregar, editar y eliminar campos calculados y de consulta.  
  
## <a name="options"></a>Opciones  
 **Agregar**  
 Agrega un nuevo campo de consulta o campo calculado al conjunto de datos.  
  
 **Eliminar**  
 Elimina el campo seleccionado del conjunto de datos.  
  
 **Nombre de campo**  
 Escriba el nombre del campo. El campo debe ser único en el conjunto de datos. Para cada campo existente en la consulta del conjunto de datos, el nombre se rellena previamente.  
  
 **Origen del campo**  
 Escriba un valor para el campo.  
  
 Para un campo calculado, el origen del campo debe ser el nombre de un campo existente recuperado por la consulta del conjunto de datos o por una expresión que cree personalmente. Por ejemplo, para crear un campo que representa 10 veces el valor en el campo de consulta Sales, utilice la expresión `=10 * Fields!Sales.Value`.  
  
 En el caso de un campo de consultas, el origen del campo debe ser el nombre de un campo existente recuperado por la consulta de conjunto de datos.  
  
 **Expresión (fx)**  
 Agregue o cambie una expresión para el campo calculado. Este botón solamente aparece cuando se hace clic en **Agregar** y se selecciona **Campo calculado**.  
  
## <a name="see-also"></a>Vea también  
 [Colección Campos del conjunto de datos &#40;Generador de informes y SSRS&#41;](report-data/dataset-fields-collection-report-builder-and-ssrs.md)   
 [Agregar datos a un informe &#40;generador de informes y SSRS&#41;](report-data/report-datasets-ssrs.md)   
 [Expresiones &#40;Generador de informes y SSRS&#41;](report-design/expressions-report-builder-and-ssrs.md)  
  
  
