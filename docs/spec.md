# Home Network Spezifikation

## Überblick
Diese Spezifikation beschreibt den erweiterten Aufbau des Home-Netzwerks mit AVM Fritz!-Komponenten für ein 7-stöckiges Gebäude.

## Verfügbare Komponenten
- 1x Fritz!Box 5590 Fiber (Hauptrouter)
- 1x Fritz! Repeater 6000 (Access Point)
- 5x Fritz! Powerline 1220 (PowerLine-Adapter)

## Gebäude-Struktur
1. **Kellergeschoss** - Glasfaseranschluss
2. **Zwischengeschoss Garage**
3. **Erdgeschoss** - SmartTV + Apple TV 4K
4. **1. Zwischengeschoss Bad**
5. **1. Obergeschoss** - Schlafen, Kinderzimmer, Büro, Dusche
6. **2. Zwischengeschoss** - Gästezimmer, Büro
7. **2. Obergeschoss** - Schlafen, Wohnen, Dachboden

## Netzwerk-Diagramm

```mermaid
graph TB
    Internet[🌐 Internet<br/>Glasfaser] --> FB[Fritz!Box 5590 Fiber<br/>Kellergeschoss<br/>Router<br/>❌ KEIN WiFi]
    
    FB --> PL1[Fritz!Powerline 1220 #1<br/>Keller]
    PL1 -.->|PowerLine über<br/>Stromnetz| PL2[Fritz!Powerline 1220 #2<br/>Erdgeschoss]
    PL2 --> REP[Fritz!Repeater 6000<br/>Erdgeschoss<br/>Access Point + WiFi]
    
    PL1 -.->|PowerLine über<br/>Stromnetz| PL3[Fritz!Powerline 1220 #3<br/>Erdgeschoss TV-Geräte]
    PL3 --> SmartTV[Samsung SmartTV<br/>Erdgeschoss]
    PL3 --> AppleTV[Apple TV 4K<br/>Erdgeschoss]
    
    PL1 -.->|PowerLine über<br/>Stromnetz| PL4[Fritz!Powerline 1220 #4<br/>2. Zwischengeschoss<br/>Gästezimmer/Büro]
    PL1 -.->|PowerLine über<br/>Stromnetz| PL5[Fritz!Powerline 1220 #5<br/>Reserve]
    
    REP -.->|WiFi Mesh| MeshRep[Fritz!Repeater<br/>1. Obergeschoss<br/>Büro]
    
    REP --> ErdgeschossWiFi[📱💻 Erdgeschoss<br/>WiFi-Clients]
    MeshRep --> ObergeschossWiFi[📱💻 1. Obergeschoss<br/>WiFi-Clients]
    PL4 --> ZwischengeschossLAN[💻 2. Zwischengeschoss<br/>LAN-Clients]
    
    classDef router fill:#e1f5fe,stroke:#0277bd,stroke-width:2px
    classDef powerline fill:#fff3e0,stroke:#ff8f00,stroke-width:2px
    classDef devices fill:#f3e5f5,stroke:#7b1fa2,stroke-width:2px
    classDef internet fill:#e8f5e8,stroke:#388e3c,stroke-width:2px
    classDef entertainment fill:#fce4ec,stroke:#c2185b,stroke-width:2px
    
    class FB,REP,MeshRep router
    class PL1,PL2,PL3,PL4,PL5 powerline
    class ErdgeschossWiFi,ObergeschossWiFi,ZwischengeschossLAN devices
    class Internet internet
    class SmartTV,AppleTV entertainment
```

## ASCII-Diagramm (für lokale Ansicht)

```
┌──────────────────────────────────────────────────────────────────────────────┐
│                      2. OBERGESCHOSS                                        │
│                   Schlafen, Wohnen, Dachboden                               │
└──────────────────────────────────────────────────────────────────────────────┘

┌──────────────────────────────────────────────────────────────────────────────┐
│                    2. ZWISCHENGESCHOSS                                       │
│                   Gästezimmer, Büro                                          │
│                                                                              │
│  ┌─────────────────────────────────────────────────────────────────────────┐ │
│  │                Fritz!Powerline 1220 #4                                 │ │
│  │              💻 LAN für Büro/Gästezimmer                               │ │
│  └─────────────────────────────────────────────────────────────────────────┘ │
│                                    │                                        │
│                                    │ PowerLine                              │
└────────────────────────────────────┼────────────────────────────────────────┘
                                     │
┌────────────────────────────────────┼────────────────────────────────────────┐
│                  1. OBERGESCHOSS   │                                        │
│           Schlafen, Kinderzimmer, Büro, Dusche                              │
│                                    │                                        │
│  ┌─────────────────────────────────────────────────────────────────────────┐ │
│  │        Fritz!Repeater (vorhandener)                                    │ │
│  │               📱💻 WiFi Mesh                                            │ │
│  └─────────────────────────────────────────────────────────────────────────┘ │
│                                    │ WiFi Mesh                              │
└────────────────────────────────────┼────────────────────────────────────────┘
                                     │
┌────────────────────────────────────┼────────────────────────────────────────┐
│                1. ZWISCHENGESCHOSS │                                        │
│                        Bad         │                                        │
└────────────────────────────────────┼────────────────────────────────────────┘
                                     │
┌────────────────────────────────────┼────────────────────────────────────────┐
│                   ERDGESCHOSS      │                                        │
│                                    │                                        │
│  ┌─────────────────────────────────┴───────────────────────────────────────┐ │
│  │              Fritz!Powerline 1220 #2                                   │ │
│  │                        │                                                │ │
│  │                        └──→ Fritz!Repeater 6000 (Access Point + WiFi)  │ │
│  └─────────────────────────────────────────────────────────────────────────┘ │
│                                                                              │
│  ┌─────────────────────────────────────────────────────────────────────────┐ │
│  │              Fritz!Powerline 1220 #3 (TV-Geräte)                      │ │
│  │                                                                         │ │
│  │  Port 1 ──→ Samsung SmartTV                                            │ │
│  │  Port 2 ──→ Apple TV 4K                                                │ │
│  └─────────────────────────────────────────────────────────────────────────┘ │
│                                                  │                          │
│                                                  │ WiFi                     │
│                                                  ▼                          │
│                                          📱💻📱 Erdgeschoss-Geräte          │
└────────────────────────────────────────┼─────────────────────────────────────┘
                                         │
                                         │ PowerLine über Stromnetz
                                         │
┌────────────────────────────────────────┼─────────────────────────────────────┐
│            ZWISCHENGESCHOSS GARAGE     │                                     │
└────────────────────────────────────────┼─────────────────────────────────────┘
                                         │
┌────────────────────────────────────────┼─────────────────────────────────────┐
│                 KELLERGESCHOSS         │                                     │
│                                        │                                     │
│            ┌─────────────────────┐     ▼                                     │
│            │ Fritz!Powerline     │  ┌─────────────────────────────────────┐  │
│            │    1220 #1          │──│     Fritz!Box 5590 Fiber           │  │
│            └─────────────────────┘  │     (Hauptrouter)                   │  │
│                                     │     ❌ KEIN WiFi                    │  │
│                                     └─────────────────────────────────────┘  │
│                                                      │                      │
│                                                      │ Glasfaser            │
│                                                      ▼                      │
│                                              🌐 Internet                    │
└──────────────────────────────────────────────────────────────────────────────┘

┌──────────────────────────────────────────────────────────────────────────────┐
│                           RESERVE                                           │
│                                                                              │
│              ┌─────────────────────────────────────────────┐                │
│              │        Fritz!Powerline 1220 #5             │                │
│              │         (für weitere Erweiterungen)        │                │
│              └─────────────────────────────────────────────┘                │
└──────────────────────────────────────────────────────────────────────────────┘
```

## Detaillierte Konfiguration

### Kellergeschoss
#### Fritz!Box 5590 Fiber
- **Betriebsart**: Router-Modus
- **Internet**: Glasfaser-Anschluss
- **DHCP**: Aktiviert (IP-Bereich: 192.168.178.1-254)
- **WiFi**: ❌ **DEAKTIVIERT** (wichtige Anforderung!)
- **Mesh**: Aktiviert für Fritz!Repeater 6000 Verbindung
- **LAN**: Port 1 für Fritz!Powerline 1220 #1
- **Funktion**: Hauptrouter, Internet-Gateway, DHCP-Server

### Erdgeschoss
#### Fritz!Powerline 1220 #2
- **Verbindung**: PowerLine zum Keller
- **LAN-Ausgang**: Fritz!Repeater 6000

#### Fritz!Powerline 1220 #3 (TV-Geräte)
- **Verbindung**: PowerLine-Netzwerk
- **LAN-Port 1**: Samsung SmartTV
- **LAN-Port 2**: Apple TV 4K

#### Fritz!Repeater 6000
- **Betriebsart**: Access Point-Modus
- **Verbindung**: LAN über PowerLine (Port 1)
- **WiFi**: Aktiviert für Erdgeschoss
- **SSID**: "HomeNetwork" (Beispiel)
- **Mesh**: Aktiviert für Verbindung zu anderen Fritz!-Geräten

#### Entertainment-Geräte
- **Samsung SmartTV**: LAN-Verbindung (PowerLine #3 Port 1)
- **Apple TV 4K**: LAN-Verbindung (PowerLine #3 Port 2)

### 1. Obergeschoss (Büro)
#### Fritz!Repeater (vorhandener)
- **Betriebsart**: Mesh-Repeater
- **Verbindung**: WiFi Mesh zum Fritz!Repeater 6000
- **WiFi**: Aktiviert für 1. Obergeschoss
- **SSID**: "HomeNetwork" (gleiche wie Erdgeschoss)
- **Abdeckung**: Schlafen, Kinderzimmer, Büro, Dusche

### 2. Zwischengeschoss (Gästezimmer/Büro)
#### Fritz!Powerline 1220 #4
- **Verbindung**: PowerLine-Netzwerk
- **LAN-Ausgang**: Für Computer/Laptops im Büro
- **Funktion**: Kabelgebundenes Internet für Arbeitsplätze

### Reserve
#### Fritz!Powerline 1220 #5
- **Status**: Nicht verwendet
- **Zweck**: Für weitere Erweiterungen verfügbar
- **Mögliche Nutzung**: Zusätzliche Stockwerke, Garten, Garage

## Netzwerk-Topologie

### IP-Adress-Schema
- **Fritz!Box**: 192.168.178.1 (Gateway)
- **Fritz!Repeater 6000**: 192.168.178.2
- **Fritz!Repeater (1. OG)**: 192.168.178.3
- **Samsung SmartTV**: 192.168.178.10
- **Apple TV 4K**: 192.168.178.11
- **PowerLine #4 (2. ZG)**: 192.168.178.4
- **DHCP-Pool**: 192.168.178.20-250

### WLAN-Konfiguration
- **SSID**: "HomeNetwork"
- **Passwort**: [Starkes Passwort]
- **Verschlüsselung**: WPA3 (oder WPA2 falls nicht unterstützt)
- **5GHz**: Aktiviert mit höherer Priorität
- **2.4GHz**: Aktiviert für Kompatibilität

### PowerLine-Konfiguration
- **Verschlüsselung**: AES 128-Bit aktiviert
- **Alle 5 Adapter**: Im gleichen PowerLine-Netzwerk
- **Geschwindigkeit**: Bis zu 1.200 Mbit/s theoretisch
- **Aufteilung**: 
  - #1: Keller (Fritz!Box)
  - #2: Erdgeschoss (Fritz!Repeater)
  - #3: Erdgeschoss (TV-Geräte)
  - #4: 2. Zwischengeschoss (Büro)
  - #5: Reserve

## Zusätzlich benötigte Komponenten

✅ **Keine zusätzlichen Komponenten nötig!**
- **LAN-Kabel** für alle Verbindungen

💡 **Optimal genutzt**: Separater PowerLine-Adapter für TV-Geräte sorgt für beste Performance, beide TV-Geräte per LAN.

## Abdeckung pro Stockwerk

| Stockwerk | Netzwerk-Typ | Gerät | Abdeckung |
|-----------|--------------|-------|-----------|
| Kellergeschoss | LAN only | Fritz!Box 5590 + PowerLine #1 | Nur LAN-Ports |
| Erdgeschoss | WiFi + LAN | Fritz!Repeater 6000 + PowerLine #2/#3 | Vollständige Abdeckung |
| 1. Obergeschoss | WiFi Mesh | Fritz!Repeater (vorh.) | Vollständige Abdeckung |
| 2. Zwischengeschoss | LAN | Fritz!Powerline 1220 #4 | Büro/Gästezimmer |
| Andere Stockwerke | WiFi | Via Mesh-Ausstrahlung | Begrenzte Abdeckung |

## Wichtige Anforderungen (Status)

✅ **Fritz!Box und Fritz!Repeater per PowerLine verbunden**

✅ **Fritz!Box WiFi deaktiviert**

✅ **Fritz!Repeater 6000 als Access Point konfiguriert**

✅ **SmartTV und Apple TV per separaten PowerLine-Adapter (LAN)**

✅ **Büro-Fritz!Repeater per WiFi Mesh verbunden**

✅ **PowerLine im 2. Zwischengeschoss für Büro**

## Vorteile dieser Lösung

- **Stabile Backbone-Verbindung**: PowerLine zwischen allen Stockwerken
- **Optimale Entertainment-Qualität**: Beide TV-Geräte per dediziertem LAN-Adapter
- **Mesh-Abdeckung**: Nahtloses WiFi in bewohnten Bereichen
- **Büro-Anbindung**: Sowohl WiFi (1. OG) als auch LAN (2. ZG)
- **Energieeffizient**: Kein unnötiges WiFi im Keller
- **Maximale Flexibilität**: 5 PowerLine-Adapter für alle Anforderungen
- **Zukunftssicher**: Reserve-Adapter für weitere Erweiterungen

## Erweiterungsmöglichkeiten

- **PowerLine #5**: Garage, Garten, Dachboden oder weiteres Stockwerk
- **Weitere Stockwerke**: Zusätzliche Mesh-Repeater
- **Mehr LAN-Ports**: Switches an PowerLine-Adaptern
- **Professionelle Arbeitsplätze**: Zusätzliche LAN-Verkabelung
- **Garten/Terrasse**: Outdoor-WiFi-Erweiterung mit PowerLine #5

## Troubleshooting

### PowerLine-Probleme
- **Keine Verbindung**: Adapter auf verschiedene Stromkreise verteilen
- **Langsame Geschwindigkeit**: Direkte Steckdose verwenden (keine Mehrfachsteckdosen)
- **Verbindungsabbrüche**: Firmware-Updates prüfen

### WiFi-Probleme
- **Schwaches Signal**: Repeater-Position optimieren
- **Mesh-Verbindung**: Automatische Kanalwahl aktivieren
- **Interferenzen**: 5GHz bevorzugen, 2.4GHz-Kanal manuell wählen

### Entertainment-Probleme
- **Streaming-Qualität**: LAN-Verbindung prüfen
- **Netzwerk-Erkennung**: DHCP-Reservierung für TV-Geräte
- **Apple TV**: Airplay-Einstellungen überprüfen
