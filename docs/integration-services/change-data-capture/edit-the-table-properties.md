---
title: Editar las propiedades de tabla | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- editTabProps
ms.assetid: 95ea72ba-8e40-4177-a963-0fb4d10c56e3
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 68e40d458f7a09d9fb073a9771aaeb9b80c6a06c
ms.sourcegitcommit: de5e726db2f287bb32b7910831a0c4649ccf3c4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/12/2018
ms.locfileid: "35332859"
---
# <a name="edit-the-table-properties"></a>Editar las propiedades de tabla
  Use este cuadro de diálogo para editar las columnas específicas de la tabla seleccionada donde se están capturando cambios. También puede editar la información de **Rol de seguridad** y de **Instancia de captura** .  
  
### <a name="to-edit-the-columns-to-include-in-the-cdc-instance"></a>Para editar las columnas que se van a incluir en la instancia CDC  
  
1.  Realice una o ambas de las acciones siguientes:  
  
    -   Active la casilla situada junto a cualquier columna adicional que desee incluir.  
  
    -   Desactive la casilla situada junto a cualquier columna que ya no desee incluir.  
  
### <a name="to-edit-the-security-role"></a>Para editar el rol de seguridad  
  
1.  Escriba un nuevo nombre o edite el nombre del rol de seguridad en el campo **Rol de seguridad** .  
  
### <a name="to-create-a-new-capture-instance"></a>Para crear una instancia de captura nueva  
  
1.  En la sección **Rol de seguridad** , en el campo **Nombre** , escriba un nombre para la instancia de captura. De forma predeterminada, el nombre especificado en el campo es el nombre de la instancia de captura actual al final del cual se ha agregado **_NEW** (por ejemplo, **instancia_anterior_NEW**).  
  
2.  Guarde la instancia de captura de una de las maneras siguientes:  
  
    -   **Nueva instancia de captura**: en este caso se guarda una nueva instancia de captura y la antigua instancia de captura no se elimina.  
  
         **Nota**: no puede tener más de dos instancias de captura por tabla. Si ya hay dos instancias de captura, esta opción no estará disponible.  
  
    -   **Reemplazar existente**: en este caso, la instancia de captura actual se elimina y se reemplaza con la instancia de captura que ha creado. Si hay dos instancias de captura definidas para esta tabla, debe seleccionar una para reemplazar.  
  
 **Nota**: puede quitar una instancia de captura de la lista de tablas en la pestaña **Tabla** .  
  
 Cuando termine de especificar la información en este cuadro de diálogo, haga clic en **Aceptar** para aceptar los cambios.  
  
## <a name="see-also"></a>Ver también  
 [Cómo editar las propiedades de la instancia CDC](../../integration-services/change-data-capture/how-to-edit-the-cdc-instance-properties.md)   
 [Realice los cambios en las tablas seleccionadas para capturar cambios ](../../integration-services/change-data-capture/make-changes-to-the-tables-selected-for-capturing-changes.md)  
  
  
