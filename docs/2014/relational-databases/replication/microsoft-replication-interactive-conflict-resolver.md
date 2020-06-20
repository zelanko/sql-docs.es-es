---
title: Solucionador interactivo de conflictos de replicación de Microsoft | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.replconflictviewer.interactiveresolver.f1
ms.assetid: d3d4a480-782b-4b1d-b839-565c8cf6cb24
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: ea6a94f79f6ae201b242fe43b32b711d5d1f561a
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85060774"
---
# <a name="microsoft-replication-interactive-conflict-resolver"></a>Solucionador interactivo de conflictos de replicación de Microsoft
  El Solucionador interactivo de conflictos se puede utilizar para las suscripciones de mezcla que se sincronizan con el Administrador de sincronización de Windows. Permite ver, comparar, modificar y seleccionar el resultado de los conflictos de datos. La replicación incluye también el Visor de conflictos, que permite ver y modificar los resultados de los conflictos una vez que se han confirmado. El Solucionador interactivo de conflictos permite seleccionar el resultado durante la sincronización.  
  
> [!NOTE]  
>  Los conflictos que implican registros lógicos no se muestran en el Solucionador interactivo. Para ver información acerca de estos conflictos, utilice procedimientos almacenados de replicación. Para obtener más información, vea [Ver información de conflictos para publicaciones de mezcla &#40;programación de la replicación con Transact-SQL&#41;](view-conflict-information-for-merge-publications.md).  
  
## <a name="options"></a>Opciones  
 **Nombre de la columna**  
 Nombre de todas las columnas de la tabla. Una o varias columnas pueden tener datos en conflicto. Independientemente de las columnas que tengan conflictos, toda la fila ganadora sobrescribirá toda la fila perdedora.  
  
 **Resolución sugerida**  
 La resolución sugerida proporcionada por el solucionador de conflictos del artículo.  
  
 **Publicador**  
 Valor de datos en el publicador.  
  
 **Suscriptor**  
 Valor de datos en el suscriptor.  
  
 **Aceptar sugerencia**, **Aceptar publicador**, y **Aceptar suscriptor**  
 Haga clic para aceptar la fila que se aplicará al publicador o al suscriptor en función del que haya perdido el conflicto. Si el publicador ha perdido el conflicto, todos los demás suscriptores recibirán la fila ganadora la próxima vez que se sincronicen con el publicador.  
  
 **Solucionar los conflictos restantes automáticamente**  
 Resuelva todos los conflictos restantes utilizando la sugerencia proporcionada por el solucionador de conflictos del artículo.  
  
 **Registrar los detalles del conflicto para consultarlos más adelante**  
 Registra los detalles del conflicto en tablas del sistema.  
  
## <a name="see-also"></a>Consulte también  
 [Resolución interactiva de conflictos](merge/advanced-merge-replication-conflict-interactive-resolution.md)   
 [Ver y resolver conflictos de datos para publicaciones de mezcla &#40;SQL Server Management Studio&#41;](view-and-resolve-data-conflicts-for-merge-publications.md)   
 [Sincronizar una suscripción mediante el Administrador de sincronización de Windows &#40;Windows Synchronization Manager&#41;](synchronize-a-subscription-using-windows-synchronization-manager.md)   
 [Replicación de mezcla avanzada: detección y resolución de conflictos](merge/advanced-merge-replication-conflict-detection-and-resolution.md)  
  
  
