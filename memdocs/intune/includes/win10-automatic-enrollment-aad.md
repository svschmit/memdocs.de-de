## <a name="enable-windows-10-automatic-enrollment"></a>Aktivieren der automatischen Registrierung von Windows 10

Durch die automatische Registrierung können Benutzer ihre Windows 10-Geräte in Intune registrieren. Benutzer müssen für die Registrierung ihr Geschäftskonto ihrem persönlichen Gerät hinzufügen oder firmeneigene Geräte mit Azure Active Directory verknüpfen. Im Hintergrund registriert sich das Gerät und tritt Azure Active Directory bei. Nach der Registrierung wird das Gerät mit Intune verwaltet.

**Voraussetzungen**

- Azure Active Directory Premium-Abonnement ([Testabonnement](https://go.microsoft.com/fwlink/?LinkID=816845))
- Microsoft Intune-Abonnement

### <a name="configure-automatic-mdm-enrollment"></a>Konfigurieren der automatischen MDM-Registrierung

1. Melden Sie sich beim [Azure-Portal](https://portal.azure.com) an, und klicken Sie auf **Azure Active Directory**.

   ![Screenshot des Azure-Portals](../enrollment/media/windows-enroll/auto-enroll-azure-main.png)

2. Wählen Sie **Mobilität (MDM und MAM)** aus.

   ![Screenshot des Azure-Portals](../enrollment/media/windows-enroll/auto-enroll-mdm.png)

3. Wählen Sie **Microsoft Intune** aus.

   ![Screenshot des Azure-Portals](../enrollment/media/windows-enroll/auto-enroll-intune.png)

4. Konfigurieren Sie den **MDM-Benutzerbereich**. Geben Sie an, welche Geräte welcher Benutzer von Microsoft Intune verwaltet werden sollen. Diese Windows 10-Geräte können sich automatisch für die Verwaltung mit Microsoft Intune registrieren.

   - **Keine**: Automatische MDM-Registrierung ist deaktiviert.
   - **Einige**: Wählen Sie die **Gruppen** aus, die ihre Windows 10-Geräte automatisch registrieren können.
   - **Alle**: Alle Benutzer können ihre Windows 10-Geräte automatisch registrieren.

      > [!IMPORTANT]
      > Für Windows BYOD-Geräte hat der MAM-Benutzerbereich Vorrang, wenn sowohl der MAM- als auch der MDM-Benutzerbereich (automatische MDM-Registrierung) für alle Benutzer (oder für die gleichen Gruppen von Benutzern) aktiviert sind. Das Gerät wird nicht beim MDM registriert, und WIP-Richtlinien (Windows Information Protection) werden angewendet, sofern Sie diese konfiguriert haben.
      >
      > Wenn Sie die automatische Registrierung für Windows BYOD-Geräte bei einem MDM aktivieren möchten, gehen Sie wie folgt vor: Legen Sie den MDM-Benutzerbereich auf **Alle** fest (oder auf **Einige**, und geben Sie eine Gruppe an) und den MAM-Benutzerbereich auf **Keine** (oder **Einige**, und geben Sie eine Gruppe an, wobei Sie sicherstellen müssen, dass Benutzer nicht Mitglied einer Gruppe sind, die sowohl für den MDM- als auch für den MAM-Benutzerbereich als Ziel verwendet wird).
      >
      >Für [unternehmenseigene Geräte](../enrollment/enrollment-restrictions-set.md#blocking-personal-windows-devices) hat der MDM-Benutzerbereich Vorrang, wenn sowohl der MDM- als auch der MAM-Benutzerbereich aktiviert ist. Das Gerät wird automatisch beim konfigurierten MDM registriert.

   > [!NOTE]
   > Der MDM-Benutzerbereich muss auf eine Azure AD-Gruppe eingestellt sein, die Benutzerobjekte enthält.

   ![Screenshot des Azure-Portals](../enrollment/media/windows-enroll/auto-enroll-scope.png)

5. Verwenden Sie die Standardwerte für die folgenden URLs:
    - **URL für MDM-Nutzungsbedingungen**
    - **URL für MDM-Ermittlung**
    - **MDM Compliance-URL**

6. Wählen Sie **Speichern** aus.

Standardmäßig ist die zweistufige Authentifizierung für den Dienst nicht aktiviert. Die zweistufige Authentifizierung wird jedoch empfohlen, wenn Sie ein Gerät registrieren. Für die zweistufige Authentifizierung müssen Sie einen Anbieter für die zweistufige Authentifizierung in Azure AD konfigurieren. Außerdem müssen Sie Ihre Benutzerkonten für die mehrstufige Authentifizierung konfigurieren. Weitere Informationen finden Sie unter [Erste Schritte mit Azure Multi-Factor Authentication-Server](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-get-started-cloud).
