---
title: Importar directivas (cuadro de diálogo) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.swb.dmf.importpolicy.f1
ms.assetid: 78ab5f6e-2f13-4788-937e-8892ef4e2345
caps.latest.revision: 21
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 1d8bcdd179434c273c37ce2bb6a00d53ea7c75b0
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36111120"
---
# <a name="import-policies-dialog-box"></a>Importar directivas (cuadro de diálogo)
  Utilice este cuadro de diálogo para importar una o varias directivas (y su condición a la que se hace referencia) que se guardaron como archivos XML, en la instancia de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] actual.  
  
## <a name="options"></a>Opciones  
 **Archivos para importar**  
 Para importar una directiva desde un archivo XML, escriba la ruta de acceso y el nombre del archivo, o use el botón Examinar (**...**).  
  
 **Reemplazar duplicados con elementos importados**  
 Seleccione esta opción para sobrescribir cualquier directiva o condición existente del mismo nombre si ya existe en esta instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)] . Una condición con una directiva dependiente no se puede sobrescribir a menos que la directiva dependiente se esté sobrescribiendo también. Si no se selecciona esta opción, una condición existente que está utilizando la misma expresión de condición no producirá un error.  
  
 **Estado de directiva**  
 Seleccione el estado que desea para la directiva importada:  
  
-   **Conservar el estado de las directivas al importar**  
  
-   **Habilitar todas las directivas al importar**  
  
-   **Deshabilitar todas las directivas al importar**  
  
## <a name="see-also"></a>Vea también  
 [Administrar servidores mediante administración basada en directivas](administer-servers-by-using-policy-based-management.md)   
 [Importar una directiva de administración basada en directivas](import-a-policy-based-management-policy.md)   
 [Exportar una directiva de administración basada en directivas](export-a-policy-based-management-policy.md)  
  
  