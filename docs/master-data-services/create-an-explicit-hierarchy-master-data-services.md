---
title: Crear una jerarquía explícita (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 04/01/2016
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: ''
ms.component: non-specific
ms.reviewer: ''
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- creating explicit hierarchies [Master Data Services]
- explicit hierarchies, creating
ms.assetid: ba768393-6990-4eda-8cb0-d58cb3cfc2e2
caps.latest.revision: 10
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b35af751769b07aba9a30c7a32cb2a452c44965c
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2018
---
# <a name="create-an-explicit-hierarchy-master-data-services"></a>Crear una jerarquía explícita (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  En [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], cree una jerarquía explícita cuando necesite una jerarquía desigual en la que los miembros puedan existir en cualquier nivel. Las jerarquías explícitas contienen los miembros de una sola entidad.  
  
 Después de crear una jerarquía explícita, puede agregarle miembros en el área funcional de **Explorador** .  
  
## <a name="prerequisites"></a>Prerequisites  
 Para realizar este procedimiento:  
  
-   Debe disponer de permiso para tener acceso al área funcional de **Administración del sistema** .  
  
-   Debe ser administrador de modelo. Para obtener más información, vea [Administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
-   La entidad debe habilitarse para las jerarquías explícitas y las colecciones.  
  
### <a name="to-create-an-explicit-hierarchy"></a>Crear una jerarquía explícita  
  
1.  En [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], haga clic en **Administración del sistema**.  
  
2.  En la página **Manage Model** (Administrar modelo), seleccione un modelo de la cuadrícula y después haga clic en **Entidades**.  
  
3.  En la página **Manage Entity** (Administrar entidad), en la cuadrícula, seleccione la fila de la entidad para la que desea crear una jerarquía explícita.  
  
4.  Haga clic en **Jerarquías explícitas**.  
  
5.  En la página **Manage Explicit Hierarchy** (Administrar jerarquía explícita), haga clic en **Agregar**.  
  
6.  En el cuadro **Nombre** , escriba un nombre para la jerarquía.  
  
7.  Opcionalmente, desactive la casilla **Mandatory hierarchy** (Jerarquía obligatoria) para crear la jerarquía como no obligatoria. Para obtener más información sobre los tipos de jerarquías, consulte [Jerarquías explícitas &#40;Master Data Services&#41;](../master-data-services/explicit-hierarchies-master-data-services.md).  
  
8.  Haga clic en **Guardar**.  
  
## <a name="grid-columns"></a>Columnas de la cuadrícula  
 Por cada jerarquía explícita creada, se agrega una fila con siete columnas a la cuadrícula. A continuación, se ofrece una descripción de las columnas.  
  
|Nombre|Description|  
|----------|-----------------|  
|Estado|El estado de la entidad. Al hacer clic en **Guardar** , aparece la imagen siguiente, que indica que la entidad se está actualizando.<br /><br /> ![Icono de estado de actualización](../master-data-services/media/mds-statusicon-updating.png "Icono de estado de actualización")<br /><br /> Si se producen errores al crear o editar una entidad, se muestra la imagen siguiente.<br /><br /> ![Icono de estado de error](../master-data-services/media/mds-statusicon-error.png "Icono de estado de error")<br /><br /> Si el estado es correcto, se muestra la siguiente imagen.<br /><br /> ![Icono de estado correcto](../master-data-services/media/mds-statusicon-ok.png "Icono de estado correcto")|  
|Nombre|Nombre de jerarquía explícita.|  
|Obligatorio|Especifica si la jerarquía explícita es obligatoria.|  
|Creado por|Nombre del usuario que creó la jerarquía explícita.|  
|Creada el|Fecha y hora en que se creó la jerarquía explícita.|  
|Actualizada por|Nombre del usuario que realizó la última actualización de la jerarquía explícita.|  
|Actualizada el|Fecha y hora en que se actualizó la jerarquía explícita por última vez.|  
  
## <a name="next-steps"></a>Next Steps  
  
-   [Crear un miembro consolidado &#40;Master Data Services&#41;](../master-data-services/create-a-consolidated-member-master-data-services.md)  
  
  
  
## <a name="see-also"></a>Ver también  
 [Jerarquías explícitas &#40;Master Data Services&#41;](../master-data-services/explicit-hierarchies-master-data-services.md)   
 [Jerarquías derivadas con límites explícitos &#40;Master Data Services&#41;](../master-data-services/derived-hierarchies-with-explicit-caps-master-data-services.md)   
 [Crear un nombre de jerarquía explícita &#40;Master Data Services&#41;](../master-data-services/change-an-explicit-hierarchy-name-master-data-services.md)  
  
  

