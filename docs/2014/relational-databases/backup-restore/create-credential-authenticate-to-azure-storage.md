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
ms.openlocfilehash: 2c5428611c67315407ed31478fbb60ccca1b6dd2
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/13/2018
ms.locfileid: "53351342"
---
# <a name="create-credential---authenticate-to-azure-storage"></a>Crear credencial - autenticarse en Azure Storage
  Use el cuadro de diálogo **Copia de seguridad en URL - Crear credencial** para crear una credencial de SQL.  
  
 Al utilizar este cuadro de diálogo para crear una credencial, debe proporcionar un certificado de administración de Windows Azure agregado al almacén de certificados local o un perfil de publicación descargado en el equipo para validar la suscripción y la información de la cuenta de almacenamiento.  
  
 **Credencial SQL**  
 Especifique el nombre de la credencial SQL que desea crear.  
  
## <a name="windows-azure-credentials"></a>Credenciales de Windows Azure  
 **Certificado de administración**  
 Use esta opción para especificar un certificado del almacén de certificados local que coincida con el certificado de administración de Windows Azure. Para obtener más información sobre el certificado de administración de Windows Azure, vea [Crear y cargar un certificado de administración de Windows Azure](https://go.microsoft.com/fwlink/?LinkId=320781).  
  
 **Suscripción**  
 Seleccione, escriba o pegue el identificador de su suscripción de Windows Azure que coincida con el certificado de administración del almacén de certificados local.  
  
 **Perfil de publicación**  
 Use esta opción si tiene un perfil de publicación descargado en el equipo. Si utiliza esta opción, el identificador de suscripción y el certificado se rellenan de forma automática.  
  
> [!CAUTION]  
>  SQL Server admite actualmente la versión 2.0 del perfil de publicación. Para descargar la versión compatible del perfil de publicación, vea [Descargar perfil de publicación 2.0](https://go.microsoft.com/fwlink/?LinkId=396421).  
  
## <a name="storage-account"></a>Cuenta de almacenamiento  
 Seleccione la cuenta de almacenamiento que desea usar para almacenar los archivos de copia de seguridad.  
  
  
