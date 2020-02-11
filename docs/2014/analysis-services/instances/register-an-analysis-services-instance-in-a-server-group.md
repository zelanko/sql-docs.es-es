---
title: Registrar una instancia de Analysis Services en un grupo de servidores | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 5fd3826b-8f75-48eb-910c-bf784163e53b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 29ecf740948d9e02d258a5daa03859d3867eb463
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66079647"
---
# <a name="register-an-analysis-services-instance-in-a-server-group"></a>Registrar una instancia de Analysis Services en un grupo de servidores
  Si tiene un gran número de instancias de servidor de Analysis Services, puede crear grupos de servidores en Management Studio para facilitar la administración de servidores. El objetivo de un grupo de servidores es proporcionar proximidad entre un grupo de servidores relacionados dentro del área de trabajo administrativo. Por ejemplo, suponga que se le encarga la tarea de administrar diez instancias independientes de Analysis Services. Agrupándolas según los criterios de tiempo de actividad y modo de servidor, o por departamento o región podría ver y conectarse a instancias que compartan las mismas características más fácilmente. También puede agregar información descriptiva que ayude a recordar cómo se utiliza el servidor.  
  
 ![Panel de servidores registrados con servidores miembro](../media/ssas-ssms-registerserver.gif "Panel de servidores registrados con servidores miembro")  
  
 Los grupos de servidores pueden crearse en una estructura jerárquica. El grupo de servidores locales es el nodo raíz. Siempre contiene las instancias de Analysis Services que se ejecutan en el equipo local. Puede agregar servidores remotos a un grupo, incluyendo el grupo local.  
  
 Después de crear un grupo de servidores, debe usar el panel Servidores registrados para ver los servidores miembro y conectarse a ellos. El panel filtra las instancias de SQL Server según el tipo de servidor (motor de base de datos, Analysis Services, Reporting Services e Integration Services). Haga clic en un tipo de servidor para ver los grupos de servidores creados para él. Para conectarse a un servidor concreto dentro del grupo, puede hacer doble clic en un servidor del grupo.  
  
 La información de conexión que se define para el servidor, incluido el nombre del servidor, se mantiene con el registro del servidor. No puede modificar la información de conexión ni usar el nombre registrado al conectarse al servidor con otras herramientas.  
  
## <a name="create-a-server-group-and-add-registered-servers"></a>Crear un grupo de servidores y agregar servidores registrados  
  
1.  En Management Studio, haga clic en Servidores registrados en el menú Ver para abrir el panel Servidores registrados en el área de trabajo. De forma predeterminada, ya se crea un grupo de servidores locales. Todas las instancias de Analysis Services que se ejecutan en el servidor local son miembros.  
  
2.  Haga clic con el botón secundario en Grupo de servidores locales, seleccione Nuevo grupo de servidores y proporcione un nombre al grupo.  
  
3.  Haga clic con el botón secundario en el grupo de servidores y seleccione Nuevo registro de servidor. Escriba el nombre de red de una instancia local o un servidor remoto, incluido el nombre de instancia si el servidor se instaló como una instancia con nombre. Opcionalmente, puede proporcionar un nombre de servidor registrado que aparezca en Servidores registrados. Este nombre se usa solo en Servidores registrados. No puede usarlo para cambiar el nombre de un servidor, ni en una cadena de conexión. Un nombre de servidor registrado puede ser más descriptivo que el nombre de servidor real o incluir otras características de identificación que ayuden a distinguir este servidor de otros.  
  
  
