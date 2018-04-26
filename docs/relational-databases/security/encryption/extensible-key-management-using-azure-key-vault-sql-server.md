---
title: Administración extensible de claves con Azure Key Vault (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 07/22/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: security
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Extensible Key Management with key vault
- Transparent Data Encryption, using EKM and key vault
- EKM, with key vault
- TDE, EKM and key vault
- Key Management with key vault
- SQL Server Connector, about
ms.assetid: 3efdc48a-8064-4ea6-a828-3fbf758ef97c
caps.latest.revision: 66
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: cd0faa90b276a4cdba63d457678d8b6c4114fe3f
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="extensible-key-management-using-azure-key-vault-sql-server"></a>Administración extensible de claves con el Almacén de claves de Azure (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  El conector de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Azure Key Vault habilita el cifrado de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para usar el servicio de Azure Key Vault como si fuera un proveedor de [Administración extensible de claves &#40;EKM&#41;](../../../relational-databases/security/encryption/extensible-key-management-ekm.md) y así proteger sus claves de cifrado de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 En este tema se describe el conector de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Hay información adicional disponible en [Pasos de instalación de Administración extensible de claves con el Almacén de claves de Azure](../../../relational-databases/security/encryption/setup-steps-for-extensible-key-management-using-the-azure-key-vault.md), [Usar el conector de SQL Server con características de cifrado de SQL](../../../relational-databases/security/encryption/use-sql-server-connector-with-sql-encryption-features.md)y [Conector de SQL Server, apéndice](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md).  
  
##  <a name="Uses"></a> ¿Qué es la Administración extensible de claves (EKM) y por qué usarla?  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] proporciona varios tipos de cifrado que ayudan a proteger información confidencial, como [cifrado de datos transparente &#40;TDE&#41;](../../../relational-databases/security/encryption/transparent-data-encryption.md), [cifrado de nivel de columna](../../../t-sql/functions/cryptographic-functions-transact-sql.md) (CLE) y [cifrado de copia de seguridad](../../../relational-databases/backup-restore/backup-encryption.md). En todos estos casos, en esta jerarquía de claves tradicional, los datos se cifran con una clave de cifrado de datos (DEK) simétrica. La clave de cifrado de datos simétrica se protege, además, cifrándose con una jerarquía de claves almacenadas en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. En lugar de este modelo, la alternativa es el modelo de proveedor EKM. El uso de la arquitectura del proveedor EKM permite a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] proteger las claves de cifrado de datos con una clave asimétrica que se almacena fuera de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en un proveedor de servicios criptográficos externo. Este modelo agrega una capa adicional de seguridad y separa la administración de claves y datos.  
   
 En la imagen siguiente se compara la jerarquía de claves de administración y servicio tradicional con el sistema del Almacén de claves de Azure.  
  
 ![ekm-key-hierarchy-traditional](../../../relational-databases/security/encryption/media/ekm-key-hierarchy-traditional.png "ekm-key-hierarchy-traditional")  
  
   
 El conector de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] actúa como puente entre [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y el Almacén de claves de Azure, por lo que [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] puede aprovechar la escalabilidad, alto rendimiento y alta disponibilidad del servicio del Almacén de claves de Azure. En la imagen siguiente se representa cómo funciona la jerarquía de claves de la arquitectura del proveedor EKM con el Almacén de claves de Azure y el conector de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
  El Almacén de claves de Azure se puede usar con instalaciones de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en máquinas virtuales de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Azure y para servidores locales. El servicio Almacén de claves también permite usar módulos de seguridad de hardware (HSM) supervisados y controlados estrechamente. Así, se obtiene un mayor grado de protección para las claves de cifrado asimétricas. Para obtener más información sobre el Almacén de claves, consulte el tema sobre el [Almacén de claves de Azure](http://go.microsoft.com/fwlink/?LinkId=521401).  
  
 En la siguiente imagen se resume el flujo de procesos de EKM usando el almacén de claves. (Los números de pasos del proceso de la imagen no se ofrecen con el fin de que coincidan con los números de los pasos de configuración que siguen a la imagen).  
  
 ![Administración extensible de claves de SQL mediante Azure Key Vault](../../../relational-databases/security/encryption/media/ekm-using-azure-key-vault.png "Administración extensible de claves de SQL mediante Azure Key Vault")  

> [!NOTE]  
>  Las versiones 1.0.0.440 y anteriores se han reemplazado y ya no se admiten en entornos de producción. Actualice a la versión 1.0.1.0 o posterior visitando el [Centro de descargas de Microsoft](https://www.microsoft.com/download/details.aspx?id=45344) y con las instrucciones de la sección "Actualización del conector de SQL Server" de la página [Conector de SQL Server, apéndice](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md) .
  
 Para ir al paso siguiente, consulte [Setup Steps for Extensible Key Management Using the Azure Key Vault](../../../relational-databases/security/encryption/setup-steps-for-extensible-key-management-using-the-azure-key-vault.md)(Pasos de instalación de Administración extensible de claves con el Almacén de claves de Azure).  
  
 Para consultar los escenarios de uso, consulte [Use SQL Server Connector with SQL Encryption Features](../../../relational-databases/security/encryption/use-sql-server-connector-with-sql-encryption-features.md)(Usar el conector de SQL Server con características de cifrado de SQL).  
  
## <a name="see-also"></a>Ver también  
 [Mantenimiento y solución de problemas del conector de SQL Server](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md)  
  
  
