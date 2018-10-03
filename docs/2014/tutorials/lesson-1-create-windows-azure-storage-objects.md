---
title: 'Lección 1: Crear objetos de Azure Storage | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: 74edd1fd-ab00-46f7-9e29-7ba3f1a446c5
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 26ab900e8a043399191e8c26314d47e48dd3e1a8
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48137385"
---
# <a name="lesson-1-create-windows-azure-storage-objects"></a>Lección 1: Crear objetos de Azure Storage
  Para poder crear copias de seguridad de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en el almacenamiento en la nube, debe crear primero una cuenta de almacenamiento y después un contenedor de blobs. La lección 1 le guía por los pasos necesarios para iniciar sesión en el portal de administración de Windows Azure, y para crear una cuenta de almacenamiento y un contenedor de blobs.  
  
## <a name="create-a-storage-account"></a>Crear una cuenta de almacenamiento  
 Para crear una cuenta de almacenamiento desde el portal de administración de Windows Azure, siga estos pasos:  
  
1.  Inicie sesión en el portal de administración de Windows Azure con su cuenta. Si no tienes una cuenta de Windows Azure, [visite evaluación gratuita de 3 meses de Windows Azure](http://go.microsoft.com/fwlink/?LinkId=271927).  
  
     ![Pantalla de inicio de sesión de Azure Windows](../../2014/tutorials/media/windowazurelogin-backuptocloud.gif "pantalla de inicio de sesión de Azure de Windows")  
  
2.  Use las instrucciones paso a paso detalladas [aquí](http://go.microsoft.com/fwlink/?LinkId=271926), para crear una cuenta de almacenamiento.  
  
3.  Vaya a la cuenta de almacenamiento que creó en el paso anterior. Desde el centro de la parte inferior de la página web, haga clic en **administrar claves**. Se mostrará la información de cuenta. Copie el nombre de la cuenta de almacenamiento y las claves de acceso. Esta información es necesaria para crear credenciales almacenadas de SQL. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usa esta información para obtener acceso a la cuenta de almacenamiento y crear copias de seguridad.  
  
     ![Captura de pantalla de claves de cuenta de almacenamiento de Windows Azure](../../2014/tutorials/media/manageaccesskeys-backuptocloud.gif "captura de pantalla de claves de cuenta de almacenamiento de Windows Azure")  
  
    > [!NOTE]  
    >  También puede crear una cuenta de almacenamiento mediante programación con las API de REST. Para obtener más información, consulte [crear cuenta de almacenamiento](http://go.microsoft.com/fwlink/?LinkId=271928).  
  
### <a name="create-a-blob-container"></a>Crear un contenedor de blobs  
 Un contenedor proporciona una agrupación de un conjunto de blobs. Todos los blobs deben estar en un contenedor. Una cuenta puede contener un número ilimitado de contenedores, pero debe tener al menos un contenedor. Un contenedor puede almacenar un número ilimitado de blobs.  
  
 Para crear un contenedor, siga estos pasos:  
  
1.  Seleccione la cuenta de almacenamiento, haga clic en el **contenedores** ficha y haga clic en **agregar contenedor** en la parte inferior de la pantalla que abre un cuadro de diálogo.  
  
     ![Crear un contenedor en el Portal de administración](../../2014/tutorials/media/backuptocloud.gif "crear un contenedor en el Portal de administración")  
  
2.  Escriba el nombre del contenedor. Anote el nombre de contenedor que especificó. Esta información se usa en la dirección URL (ruta de acceso al archivo de copia de seguridad) en las instrucciones T-SQL de las lecciones 3 y 4.  
  
3.  Seleccione privado para **tipo de acceso**. Se recomienda crear contenedores privados para proteger los archivos de copia de seguridad.  
  
     ![Crear un nuevo contenedor de blob](../../2014/tutorials/media/backuptocloud-newblobcontainer.gif "crear un nuevo contenedor de blob")  
  
    > [!NOTE]  
    >  La autenticación en la cuenta de almacenamiento es necesaria para las copias de seguridad y la restauración de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] incluso aunque elija crear un contenedor público.  
    >   
    >  También puede crear un contenedor mediante programación con las API de REST. Para obtener más información, consulte [crear contenedor](http://go.microsoft.com/fwlink/?LinkId=271946).  
  
### <a name="next-lesson"></a>Lección siguiente  
 [Lección 2: Crear una credencial de SQL Server](../../2014/tutorials/lesson-2-create-a-sql-server-credential.md).  
  
  
