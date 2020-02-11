---
title: Guardar metadatos (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 9e49c25f-9216-43f4-8e99-2eaab298e215
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: 7e45f85a26d2beaaba552707681e574bae4795cc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68266507"
---
# <a name="save-metadata--oracletosql"></a>Guardar metadatos (OracleToSQL)
El cuadro de diálogo **guardar metadatos** le solicita que cargue los metadatos en el proyecto de SSMA antes de guardarlo. Esto le permite tener un archivo de proyecto completo que puede usar sin conexión y enviar a otras personas, como personal de soporte técnico.  
  
Para tener acceso al cuadro de diálogo **guardar metadatos** , guarde el proyecto. Si faltan metadatos, SSMA mostrará el cuadro de diálogo **guardar metadatos** .  
  
## <a name="options"></a>Opciones  
**Nombre**  
El nombre de cada base de datos del proyecto.  
  
**Estado**  
Indica si los metadatos se cargan en el proyecto de SSMA o si faltan metadatos.  
  
SSMA carga los metadatos en el proyecto según sea necesario. Los metadatos se cargan automáticamente al examinar los metadatos y convertir los esquemas.  
  
**Seleccionar todo**  
Selecciona todas las bases de datos de la lista.  
  
**Borrar**  
Desactiva la casilla para todas las bases de datos con metadatos que faltan. No puede desactivar la casilla si se han cargado los metadatos.  
  
**Guardar**  
Guarda el proyecto y carga los metadatos de las bases de datos seleccionadas que tienen metadatos que faltan.  
  
**Cancelar**  
Cancela la operación de guardar. Los metadatos que faltan no se cargan en el proyecto.  
  
