---
title: Función LocalDBShareInstance | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
api_name:
- LocalDBShareInstance
api_location:
- sqluserinstance.dll
topic_type:
- apiref
ms.assetid: 21eb3b9a-7d32-455b-89bb-f624198cd202
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 1fc8b4e5a5d6741dd11faf4c846db7862a7254db
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85027614"
---
# <a name="localdbshareinstance-function"></a>Función LocalDBShareInstance
  Comparte la instancia de SQL Server Express LocalDB especificada con otros usuarios del equipo, mediante el nombre compartido indicado.  
  
 **Archivo de encabezado:** sqlncli.h  
  
## <a name="syntax"></a>Sintaxis  
  
```  
HRESULT LocalDBShareInstance(  
           PSID pOwnerSID,  
           PCWSTR pInstancePrivateName,  
           PCWSTR pInstanceSharedName,   
           DWORD dwFlags   
);  
```  
  
## <a name="parameters"></a>Parámetros  
 *pOwnerSID*  
 [Entrada] SID del propietario de la instancia.  
  
 *pInstancePrivateName*  
 [Entrada] Nombre privado de la instancia de LocalDB que se va a compartir.  
  
 *pInstanceSharedName*  
 [Entrada] Nombre de la instancia compartida de LocalDB que se va a compartir.  
  
 *dwFlags*  
 [Entrada] Reservado para uso futuro. En estos momentos, se debe establecer en 0.  
  
## <a name="returns"></a>Devoluciones  
 S_OK  
 La función se ha realizado correctamente.  
  
 [LOCALDB_ERROR_NOT_INSTALLED](../express-localdb-error-messages/localdb-error-not-installed.md)  
 SQL Server Express LocalDB no está instalado en el equipo.  
  
 [LOCALDB_ERROR_INVALID_PARAMETER](../express-localdb-error-messages/localdb-error-invalid-parameter.md)  
 Uno o más parámetros de entrada especificados no son válidos.  
  
 [LOCALDB_ERROR_INVALID_INSTANCE_NAME](../express-localdb-error-messages/localdb-error-invalid-instance-name.md)  
 El nombre de instancia de especificado no es válido.  
  
 [LOCALDB_ERROR_UNKNOWN_INSTANCE](../express-localdb-error-messages/localdb-error-unknown-instance.md)  
 La instancia especificada no existe.  
  
 [LOCALDB_ERROR_ADMIN_RIGHTS_REQUIRED](../express-localdb-error-messages/localdb-error-admin-rights-required.md)  
 Se requieren privilegios de administrador para ejecutar esta operación.  
  
 [LOCALDB_ERROR_SHARED_NAME_TAKEN](../express-localdb-error-messages/localdb-error-shared-name-taken.md)  
 El nombre compartido especificado ya existe.  
  
 [LOCALDB_ERROR_INSTANCE_ALREADY_SHARED](../express-localdb-error-messages/localdb-error-instance-already-shared.md)  
 Ya se está compartiendo la instancia especificada.  
  
 [LOCALDB_ERROR_INTERNAL_ERROR](../express-localdb-error-messages/localdb-error-internal-error.md)  
 Se ha producido un error inesperado. Vea el registro de eventos para obtener detalles.  
  
## <a name="remarks"></a>Comentarios  
 Para obtener un ejemplo de código que utilice LocalDB API, vea [SQL Server Express LocalDB Reference](../sql-server-express-localdb-reference.md).  
  
## <a name="see-also"></a>Consulte también  
 [Información de encabezado y versión de SQL Server Express LocalDB](sql-server-express-localdb-header-and-version-information.md)  
  
  
