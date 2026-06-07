# Supervisory PLC TIA-Portal S7-1215C KTP400  

Developed entirely in TIA Portal v15.1 using Structured Text (SCL), with no third-party libraries.  
The function block is fully optimized for the S7-1215C AC/DC/Rly, keeping a lean and maintainable structure with room for future expansion.  
> This is a simulation version of a supervisory system for multi-tank volume monitoring, close to industrial needs but operating without real analog signals — all level inputs are entered manually via HMI.  

⚠️ CAUTION: NO EMERGENCY CONTROL LOGIC IS IMPLEMENTED  

---

## 🚀 System Overview  

This project implements a multi-tank volume supervisory system, featuring:  

Multi-Tank Volume Calculation (Simulation): Reads level inputs (0–100%) for 4 tank buffers entered manually via HMI, with built-in safety clamping to keep each buffer within valid bounds. No real analog signals are read.  
Total Volume Aggregation: Combines all 4 buffer levels and converts the result into a total volume in m³, based on cylindrical tank geometry (r = 0.25 m, h = 5 m per tank).  
Three-State Status Logic: A CASE block evaluates the total volume against Low (0–30%), OK (30–90%), and High (90–100%) thresholds, activating the corresponding HMI indicator (H1/H2/H3).    
HMI Color-Coded Status Display: The "System Level" label changes dynamically — Red blink for Low, White for OK, and Orange blink for High — giving the operator an immediate visual reference.  
HMI Update & Reset Control: The calculation loop is triggered by an HMI_UPDATE flag and can be fully reset via HMI_RESET, clearing the total volume display.  
Safety Envelopes: Each individual buffer is clamped to [0, 100] before being included in the volume calculation.  

---

## 🛠 Hardware Stack  

PLC: Siemens S7-1215C AC/DC/Rly  
HMI: Siemens KTP400 Basic  
Development Environment: TIA Portal v15.1  
Language: Structured Control Language (SCL / Structured Text)  
Level Input: Manual entry via HMI (simulation — no physical LIT sensors connected)  

---

## 📂 Project Structure  

```
/PLC Program      — .zip file with full TIA Portal v15.1 PLC project (ready to open and download)
                  + Standalone copy of the SCL source code for quick review  
/PLC TAGS         — LibreOffice (.ods) and Excel (.xls) files with the PLC tags table  
/Screenshots      — HMI screenshots and TIA Portal configuration views
```

---

## ⚙ Operational Flow  

HMI Update: Operator enters level (%) for each of the 4 tanks and triggers UPDATE to recalculate total volume in m³.  
HMI Reset: Triggering RESET clears the total volume and returns the display to zero.  
Low Level (0–30%): H1 Red active — HMI label displays "System Level: Low" blinks in Red.  
Normal Level (30–90%): H2 Green active — HMI label displays "System Level: OK" in White.  
High Level (90–100%): H3 Yellow active — HMI label displays "System Level: High" blinks in Orange.  
Volume Calculation: Total Volume (m³) = (Sum of 4 buffer levels × 3927) / 400 — based on cylindrical geometry per tank.  
⚠️ CAUTION: NO EMERGENCY CONTROL IS IMPLEMENTED.  

---

## 📜 License

This project is licensed under the GNU General Public License v3.0 (GPL-3.0).  
See the full license text at: https://www.gnu.org/licenses/gpl-3.0.html.

---

☕ If this project is helpful for your application, please consider supporting:<br> 
https://www.paypal.com/donate/?hosted_button_id=8S8BJ9TT368VN  

Built by **rafamuratt**: https://murat-tech.eu/  
Murat-Tech Channel: https://www.youtube.com/@Murat-TechChannel-EN
