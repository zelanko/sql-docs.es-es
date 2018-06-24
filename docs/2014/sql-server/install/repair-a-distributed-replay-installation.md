---
title: Reparar una instalación de Distributed Replay | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 6fcd8ca8-1ceb-457d-9545-096c74e274d7
caps.latest.revision: 9
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 8adf917831b33c1603b3c0c4a1e7b678900cf7dd
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36196169"
---
# <a name="repair-a-distributed-replay-installation"></a>Reparar una instalación de Distributed Replay
  La reparación de un componente de Distributed Replay (controlador o cliente) hará lo siguiente:  
  
1.  Instale todos los archivos asociados en el disco de nuevo y reemplace los archivos existentes.  
  
2.  Volver a crear la cuenta de servicio de Windows si la cuenta de servicio correspondiente se ha quitado.  
  
 No puede utilizar la operación de reparación para agregar o quitar componentes. Para agregar o quitar componentes, active o desactive el componente correspondiente en el árbol de características de la página **Selección de características** del programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
### <a name="to-repair-a-failed-installation-of-distributed-replay"></a>Para reparar una instalación de Distributed Replay con errores  
  
1.  En el menú **Inicio** , haga clic en **Panel de control**y haga doble clic en **Agregar o quitar programas**.  
  
2.  Seleccione [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] en la ventana **Desinstalar o  cambiar un programa** y, a continuación, en el cuadro de diálogo [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , haga clic en **Reparar**.  
  
3.  Siga los pasos del asistente para la instalación de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] y, en la página **Seleccionar características** , seleccione los componentes de Distributed Replay que desea reparar. A continuación, haga clic en **Siguiente**.  
  
4.  Complete el Asistente para la instalación de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] para reparar las características de Distributed Replay seleccionadas.  
  
  