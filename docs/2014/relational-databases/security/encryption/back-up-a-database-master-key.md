---
title: Hacer copias de seguridad de una clave maestra de una base de datos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- database master key [SQL Server], exporting
ms.assetid: 7ad9a0a0-6e4f-4f7b-8801-8c1b9d49c4d8
author: aliceku
ms.author: aliceku
manager: craigg
ms.openlocfilehash: 5f1eeab5d0c3dfae008bbcecc3fe8d89d2c7e2c5
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48186865"
---
# <a name="back-up-a-database-master-key"></a>Hacer copias de seguridad de una clave maestra de una base de datos
  En este tema se describe cómo realizar una copia de seguridad de la clave maestra de una base de datos en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mediante [!INCLUDE[tsql](../../../includes/tsql-md.md)]. La clave maestra de una base de datos se usa para cifrar otras claves y certificados de la base de datos Si se elimina o daña, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] podría ser incapaz de descifrar esas claves y los datos cifrados que las utilizan quedarían inutilizables y perdidos. Por ello, se debe hacer una copia de seguridad de la clave maestra de la base de datos y guardar la copia de seguridad en un lugar protegido fuera de las instalaciones.  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Seguridad](#Security)  
  
-   [Para realizar una copia de seguridad de la clave maestra de una base de datos mediante Transact-SQL](#Procedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
  
-   Es necesario abrir la clave maestra y, por tanto, descifrarla antes de realizar una copia de seguridad de la misma. Si está cifrada con la clave maestra de servicio, no es necesario abrir explícitamente la clave maestra. Pero si la clave maestra solo está cifrada con una contraseña, debe abrirse explícitamente.  
  
-   Se recomienda realizar una copia de seguridad de la clave maestra inmediatamente después de crearla y guardarla en un lugar seguro y alejado de las instalaciones.  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permissions  
 Necesita el permiso CONTROL en la base de datos.  
  
##  <a name="Procedure"></a> Usar SQL Server Management Studio con Transact-SQL  
  
#### <a name="to-back-up-the-database-master-key"></a>Para hacer una copia de seguridad de la clave maestra de una base de datos  
  
1.  En [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], conéctese a la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que contenga la clave maestra de base de datos de la que desea hacer una copia de seguridad.  
  
2.  Elija una contraseña que se utilizará para cifrar la clave maestra de base de datos en el medio de la copia de seguridad. Esta contraseña se somete a comprobaciones de complejidad.  
  
3.  Hágase con un medio de copia de seguridad extraíble para guardar una copia de seguridad de la clave.  
  
4.  Identifique un directorio NTFS en el que va a crear la copia de seguridad de la clave. En este directorio creará el archivo indicado en el paso siguiente. El directorio debe estar protegido mediante listas de control de acceso (ACL) muy restrictivas.  
  
5.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
6.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
7.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```  
    -- Creates a backup of the "AdventureWorks2012" master key. Because this master key is not encrypted by the service master key, a password must be specified when it is opened.  
    USE AdventureWorks2012;   
    GO  
    OPEN MASTER KEY DECRYPTION BY PASSWORD = 'sfj5300osdVdgwdfkli7';   
  
    BACKUP MASTER KEY TO FILE = 'c:\temp\exportedmasterkey'   
        ENCRYPTION BY PASSWORD = 'sd092735kjn$&adsg';   
    GO  
    ```  
  
    > [!NOTE]  
    >  La ruta de acceso de archivo a la clave y la contraseña de la clave (si existe) serán distintas de las que se indica más arriba. Asegúrese de que ambas son específicas para la instalación del servidor y de la clave.  
  
8.  Copie el archivo en el medio de copia de seguridad y compruebe que la copia es correcta.  
  
9. Guarde la copia de seguridad en una ubicación segura fuera de las instalaciones.  
  
 Para obtener más información, vea [OPEN MASTER KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/open-master-key-transact-sql) y [BACKUP MASTER KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-master-key-transact-sql).  
  
  
