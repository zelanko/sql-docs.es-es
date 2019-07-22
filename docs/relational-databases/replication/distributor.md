---
title: Distribuidor | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.replicationutilities.selectdistributor.f1
ms.assetid: 787f0e9c-09dd-438a-bc04-5b8f99c127b8
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 910402b059f602d68428f5348ce35921942d918e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68128261"
---
# <a name="distributor"></a>Distribuidor
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  La página **Distribuidor** aparece en el Asistente para configurar la distribución y en el Asistente para nueva publicación. El distribuidor es un servidor que contiene la base de datos de distribución y almacena los metadatos y los datos del historial para todos los tipos de replicación. El distribuidor también almacena las transacciones para la replicación transaccional. El distribuidor puede ser el mismo servidor que el publicador (distribuidor local) o un servidor independiente del publicador (distribuidor remoto). El rol del distribuidor varía según el tipo de replicación implementada. Por lo general, es mayor el rol para la replicación transaccional que para la replicación de mezcla y de instantáneas. Las replicaciones de mezcla y de instantáneas usan generalmente un distribuidor local, pero la replicación transaccional en un sistema muy ocupado puede beneficiarse de usar un distribuidor remoto.  
  
 El distribuidor utiliza estos recursos adicionales en el servidor en el que se encuentra:  
  
-   Espacio de disco adicional si los archivos de instantáneas para la publicación se almacenan en éste (lo que ocurre habitualmente).  
  
-   Espacio de disco adicional para almacenar la base de datos de distribución.  
  
-   Uso adicional del procesador por los agentes de replicación para las suscripciones de inserción que se ejecutan en el distribuidor  
  
 El servidor seleccionado como distribuidor debe disponer del espacio en disco y la capacidad de proceso adecuados para la replicación y cualquier otra actividad asignada a ese servidor.  
  
## <a name="options"></a>Opciones  
 **'\<nombreDeServidor>' actuará como su propio distribuidor; SQL Server creará una base de datos y un registro de distribución.**  
 Seleccione esta opción para configurar el servidor al que está conectado como distribuidor.  
  
 **Utilizar el siguiente servidor como distribuidor  (Nota: el servidor que selecciona debe estar previamente configurado como distribuidor)**  
 Seleccione esta opción y haga clic en el nombre de uno de los servidores que se muestran a continuación para configurar otro servidor como distribuidor.  
  
 **Agregar**  
 Si no se muestra el servidor que desea usar como distribuidor, haga clic en **Agregar** para identificar el servidor y agregarlo a la lista.  
  
> [!NOTE]  
>  Para usar un servidor remoto como distribuidor, el servidor remoto debe estar configurado como distribuidor. Debe habilitar el servidor con el que se ejecuta el asistente como publicador en dicho distribuidor.  
  
## <a name="see-also"></a>Consulte también  
 [Configurar distribución](../../relational-databases/replication/configure-distribution.md)   
 [Configurar la publicación y la distribución](../../relational-databases/replication/configure-publishing-and-distribution.md)  
  
  
