---
title: "Cuadro de diálogo Evaluar directivas, página Selección de directiva | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.swb.dmf.runnow.f1
ms.assetid: 20075fbe-0b48-42c8-b747-690f1aa23dcf
caps.latest.revision: "36"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a20a0491a0c5aa08b9c8688b3cbc20d94340f7d2
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="evaluate-policies-dialog-box-policy-selection-page"></a>Cuadro de diálogo Evaluar directivas, página Selección de directiva
  Utilice este cuadro de diálogo para evaluar las directivas de administración basada en directivas. Al seleccionar la página **Resultados de la evaluación** , puede aplicar directivas a los elementos de un conjunto de destinos que no cumplen las directivas.  
  
## <a name="options"></a>Opciones  
 **Origen**  
 Especifica el origen de las directivas. Para cambiar el origen, haga clic en el botón Examinar (**...**) para abrir el cuadro de diálogo **Seleccionar origen** .  
  
 **Archivos**  
 Escriba la ruta de acceso de un archivo que contenga una directiva de administración basada en directivas, o use el botón Examinar (**...**) para seleccionar el archivo.  
  
 **Server**  
 Seleccione esta opción para conectarse a una instancia del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] que contenga la directiva que desea.  
  
 **Directivas: Directiva**  
 Haga clic en esta opción para abrir el cuadro de diálogo de directiva correspondiente a la directiva especificada.  
  
 **Directivas: Categoría**  
 Categoría de la directiva. Este cuadro es de solo lectura.  
  
 **Directivas: Faceta**  
 Faceta implementada por la directiva. Este cuadro es de solo lectura.  
  
 **Evaluar**  
 Ejecuta la directiva en modo de evaluación. De esta forma se genera un informe de compatibilidad para el conjunto de destino, pero no se vuelve a configurar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ni se exige la compatibilidad en el futuro.  
  
## <a name="possible-errors"></a>Errores posibles  
  
-   **No se encontraron destinos**  
  
     El conjunto de destino podría estar vacío debido a alguna de las razones siguientes:  
  
    -   No hay ningún destino en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] del tipo especificado por la directiva.  
  
    -   La restricción de servidor podría excluir la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que contiene el destino.  
  
    -   Si la directiva está en un objeto de una base de datos (por ejemplo una tabla, vista o usuario), la base de datos podría no suscribirse a la categoría de la directiva.  
  
    -   El filtro del conjunto de destino podría excluir todos los destinos de esta instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
    -   El tipo de servidor de destino es diferente del tipo de servidor en el que se evalúa la directiva. Por ejemplo, en [!INCLUDE[ssDE](../../includes/ssde-md.md)], si intenta evaluar una directiva creada para [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], recibirá un conjunto de destinos vacío.  
  
## <a name="see-also"></a>Vea también  
 [Administrar servidores mediante administración basada en directivas](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)   
 [Cuadro de diálogo Evaluar directivas, página Resultados de la evaluación](../../relational-databases/policy-based-management/evaluate-policies-dialog-box-evaluation-results-page.md)  
  
  
