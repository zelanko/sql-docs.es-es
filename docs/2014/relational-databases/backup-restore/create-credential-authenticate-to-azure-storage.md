---
title: Creación de una credencial - autenticarse en Azure Storage | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql12.swb.backuptourl.createcred.f1
ms.assetid: 0622619d-27c5-4ff0-83e5-cde31648c27a
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 62ab149ad9bd20c9c33c416f46ec18b01356fd10
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48204935"
---
# <a name="create-credential---authenticate-to-azure-storage"></a>Crear credencial - autenticarse en Azure Storage
  Utilice el cuadro de diálogo **Copia de seguridad en URL - Crear credencial** para crear una nueva credencial de SQL.  
  
 Al utilizar este cuadro de diálogo para crear una credencial, debe proporcionar un certificado de administración de Windows Azure agregado al almacén de certificados local o un perfil de publicación descargado en el equipo para validar la suscripción y la información de la cuenta de almacenamiento.  
  
 **Credencial SQL**  
 Especifique el nombre de la credencial SQL que desea crear.  
  
## <a name="windows-azure-credentials"></a>Credenciales de Windows Azure  
 **Certificado de administración**  
 Use esta opción para especificar un certificado del almacén de certificados local que coincida con el certificado de administración de Windows Azure. Para obtener más información sobre el certificado de administración de Windows Azure, vea [Crear y cargar un certificado de administración de Windows Azure](http://go.microsoft.com/fwlink/?LinkId=320781).  
  
 **Suscripción**  
 Seleccione, escriba o pegue el identificador de su suscripción de Windows Azure que coincida con el certificado de administración del almacén de certificados local.  
  
 **Perfil de publicación**  
 Use esta opción si tiene un perfil de publicación descargado en el equipo. Si utiliza esta opción, el identificador de suscripción y el certificado se rellenan de forma automática.  
  
> [!CAUTION]  
>  SQL Server admite actualmente la versión 2.0 del perfil de publicación. Para descargar la versión compatible del perfil de publicación, vea [Descargar perfil de publicación 2.0](http://go.microsoft.com/fwlink/?LinkId=396421).  
  
## <a name="storage-account"></a>Cuenta de almacenamiento  
 Seleccione la cuenta de almacenamiento que desea usar para almacenar los archivos de copia de seguridad.  
  
  
