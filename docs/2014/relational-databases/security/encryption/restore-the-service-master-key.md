---
title: Restaurar la clave maestra de servicio | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- service master key [SQL Server], importing
- service master key [SQL Server], restoring
ms.assetid: 14bdbbbe-d384-4692-b670-4243d2466fe1
author: jaszymas
ms.author: jaszymas
manager: craigg
ms.openlocfilehash: 21abdf4e5781f179c8168ff02aa611bd7dffd39f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "74957180"
---
# <a name="restore-the-service-master-key"></a>Restaurar la clave maestra de servicio
  En este tema se describe cómo restaurar la clave maestra de servicio en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mediante [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
> [!WARNING]  
>  Es improbable que alguna vez deba restaurar la clave maestra de servicio. Si tiene que hacerlo, debe proceder con mucha precaución. Para obtener más información, consulte [Back Up the Service Master Key](service-master-key.md).  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Seguridad](#Security)  
  
-   [Para restaurar la clave maestra de servicio utilizando Transact-SQL](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
  
-   Al restaurar la clave maestra de servicio, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] descifra todas las claves y secretos cifrados con la clave maestra de servicio actual y, a continuación, los cifra con la clave maestra de servicio cargada desde el archivo de copia de seguridad.  
  
-   Si se producen errores durante cualquier descifrado, se producirán errores en la restauración. Puede utilizar la opción FORCE para omitir los errores, pero esta opción provocará la pérdida de los datos que no sea posible descifrar.  
  
-   La regeneración de la jerarquía de cifrado es una operación que requiere un uso intensivo de recursos. Debe programarla durante un período de baja demanda.  
  
> [!CAUTION]  
>  La clave maestra de servicio es la raíz de la jerarquía de cifrado de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . La clave maestra de servicio protege directa o indirectamente las demás claves del árbol. Si no es posible descifrar una clave dependiente durante una restauración forzada, se perderán los datos que protege la clave.  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 Requiere el permiso CONTROL SERVER en el servidor.  
  
##  <a name="SSMSProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-restore-the-service-master-key"></a>Para restaurar la clave maestra de servicio  
  
1.  Recupere una copia de seguridad de la clave maestra de servicio, ya sea desde un medio físico de copia de seguridad o desde un directorio del sistema de archivos local.  
  
2.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
3.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
4.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```  
    -- Restores the service master key from a backup file.  
    RESTORE SERVICE MASTER KEY   
        FROM FILE = 'c:\temp_backups\keys\service_master_key'   
        DECRYPTION BY PASSWORD = '3dH85Hhk003GHk2597gheij4';  
    GO  
    ```  
  
    > [!NOTE]  
    >  La ruta de acceso de archivo a la clave y la contraseña de la clave (si existe) serán distintas de las que se indica más arriba. Asegúrese de que ambas son específicas para la instalación del servidor y de la clave.  
  
  
