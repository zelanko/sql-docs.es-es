---
title: Solucionador interactivo de conflictos de replicación de Microsoft | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.replconflictviewer.interactiveresolver.f1
ms.assetid: d3d4a480-782b-4b1d-b839-565c8cf6cb24
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 62d63299c05ea17d57130fcad7d81af417b78610
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47619883"
---
# <a name="microsoft-replication-interactive-conflict-resolver"></a>Solucionador interactivo de conflictos de replicación de Microsoft
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  El Solucionador interactivo de conflictos se puede utilizar para las suscripciones de mezcla que se sincronizan con el Administrador de sincronización de Windows. Permite ver, comparar, modificar y seleccionar el resultado de los conflictos de datos. La replicación incluye también el Visor de conflictos, que permite ver y modificar los resultados de los conflictos una vez que se han confirmado. El Solucionador interactivo de conflictos permite seleccionar el resultado durante la sincronización.  
  
> [!NOTE]  
>  Los conflictos que implican registros lógicos no se muestran en el Solucionador interactivo. Para ver información acerca de estos conflictos, utilice procedimientos almacenados de replicación. Para obtener más información, vea [Ver información de conflictos para publicaciones de mezcla &#40;programación de la replicación con Transact-SQL&#41;](../../relational-databases/replication/view-conflict-information-for-merge-publications.md).  
  
## <a name="options"></a>Opciones  
 **Nombre de columna**  
 Nombre de todas las columnas de la tabla. Una o varias columnas pueden tener datos en conflicto. Independientemente de las columnas que tengan conflictos, toda la fila ganadora sobrescribirá toda la fila perdedora.  
  
 **Resolución sugerida**  
 La resolución sugerida proporcionada por el solucionador de conflictos del artículo.  
  
 **publicador**  
 Valor de datos en el publicador.  
  
 **Suscriptor**  
 Valor de datos en el suscriptor.  
  
 **Aceptar sugerencia**, **Aceptar publicador**, y **Aceptar suscriptor**  
 Haga clic para aceptar la fila que se aplicará al publicador o al suscriptor en función del que haya perdido el conflicto. Si el publicador ha perdido el conflicto, todos los demás suscriptores recibirán la fila ganadora la próxima vez que se sincronicen con el publicador.  
  
 **Solucionar los conflictos restantes automáticamente**  
 Resuelva todos los conflictos restantes utilizando la sugerencia proporcionada por el solucionador de conflictos del artículo.  
  
 **Registrar los detalles del conflicto para consultarlos más adelante**  
 Registra los detalles del conflicto en tablas del sistema.  
  
## <a name="see-also"></a>Ver también  
 [Resolución interactiva de conflictos](../../relational-databases/replication/merge/advanced-merge-replication-conflict-interactive-resolution.md)   
 [Ver y resolver conflictos de datos para publicaciones de mezcla &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/view-and-resolve-data-conflicts-for-merge-publications.md)   
 [Sincronizar una suscripción mediante el Administrador de sincronización de Windows &#40;Windows Synchronization Manager&#41;](../../relational-databases/replication/synchronize-a-subscription-using-windows-synchronization-manager.md)   
 [Replicación de mezcla avanzada: detección y resolución de conflictos](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)  
  
  
