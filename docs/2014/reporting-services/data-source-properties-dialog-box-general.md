---
title: Cuadro de diálogo de propiedades General del origen de datos | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.datasourceproperties.general.f1
- "10120"
ms.assetid: 44b5edd3-5c11-4d3d-91b8-5871aa0572ed
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 7db7aa857e695e35dee5125cdfed1effe3dd1852
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/22/2019
ms.locfileid: "59949431"
---
# <a name="data-source-properties-dialog-box-general"></a>Propiedades del origen de datos (cuadro de diálogo), General
  Seleccione **General** en el cuadro de diálogo **Propiedades del origen de datos** para mostrar y modificar la información de conexión de un origen de datos del informe.  
  
## <a name="options"></a>Opciones  
 **Name**  
 Escriba el nombre del origen de datos. Dicho nombre debe ser único en el informe. De forma predeterminada, al origen de datos se le asigna un nombre general, como DataSource1 o DataSource2.  
  
 **Conexión incrustada**  
 Seleccione esta opción si no desea utilizar un origen de datos compartido.  
  
 **Tipo**  
 Seleccione una extensión de procesamiento de datos. En la lista se muestran todas las extensiones registradas.  
  
 **Cadena de conexión**  
 Escriba una cadena de conexión para el origen de datos. Haga clic en **Editar** para generar la cadena de conexión mediante el cuadro de diálogo **Propiedades de conexión** . Haga clic en el botón **Expresiones** (*fx*) para editar la expresión.  
  
 **Utilizar referencia de origen de datos compartido**  
 Seleccione esta opción para establecer un vínculo con un origen de datos compartido. Seleccione un origen de datos compartido en la lista desplegable. Para editar el origen de datos seleccionado, haga clic en **Editar**. Si se selecciona **Utilizar referencia de origen de datos compartido** , **Tipo** y **Cadena de conexión** se deshabilitan.  
  
 **Usar una sola transacción al procesar las consultas**  
 Seleccione esta opción para indicar que los conjuntos de datos que usan este origen de datos deben ejecutarse en una sola transacción en la base de datos. Para incluir transacciones para subinformes que usan el mismo origen de datos, establezca **MergeTransactions** en **True** en la sección de propiedades **Otros** del panel **Propiedades** del subinforme.  
  
## <a name="see-also"></a>Vea también  
 [Agregar datos a un informe &#40;generador de informes y SSRS&#41;](report-data/report-datasets-ssrs.md)   
 [Crear un origen de datos incrustado o compartido &#40;SSRS&#41;](../../2014/reporting-services/create-an-embedded-or-shared-data-source-ssrs.md)   
 [Conexiones de datos, orígenes de datos y cadenas de conexión en Reporting Services](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-reporting-services.md)   
 [Propiedades del origen de datos (cuadro de diálogo), Credenciales](../../2014/reporting-services/data-source-properties-dialog-box-credentials.md)  
  
  
