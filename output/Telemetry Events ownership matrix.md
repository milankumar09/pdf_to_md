Source tag : https://rndwiki.inc.hpicorp.net/confluence/spaces/CDM/pages/1170244140/Telemetry+Events+ownership+matrix

Note : This extracted file is generated from SharePoint or Wiki content. If the source document contains images, charts, or graphical elements, they may not be fully converted into Markdown format. For complete clarity, please refer to the original source using the source tag provided above.

# Telemetry Events ownership matrix

Sirius Product line (JIRA SIRIUSFW) (TPM: prashanth.nilogal@hp.com)
Apollo/Horizon Product Line (JIRA SMBFW) (TPM: shreevathsa.jayadeva@hp.com)
Jedi Product Line (JIRA JOLT) (TPM: nagaraj.padshetty@hp.com)
Dune Product Line (JIRA DUNE) (TPM: kanghoon.lee@hp.com)
Ares Product Line (JIRA Low Ink Firmware) (TPM: saurabh.srivastava2@hp.com)

Sirius Product line (JIRA SIRIUSFW) (TPM: prashanth.nilogal@hp.com)

| EventCategory | Primary/Secondary owners | Scope/Platform inclusions |
|---|---|---|
| fwUpdate | Mahitha Maheswari | |
| supply | rodney.tay@hp.com, kiran.kum.p-n@hp.com | |
| errorRecovery | sook-shin.chang@hp.com | |
| systemError | vinod.pattanashetti1@hp.com | Watt LE: yi-xiong-anselm.lim@hp.com CuXLP : suresh-kumar.ravi@hp.com Mimas15 : rongmei.xiao@hp.com Includes both FW asserts and HW failure |
| printHead | rodney.tay@hp.com | |
| jobStatus (deprecated) | IPP: tarak.parikh@hp.com other: pooja-j.nayak@hp.com | Deprecated since Dec 2022 |
| calibration | wei.liang.low1@hp.com | |
| jobError | zyn-ming.lai@hp.com | For Watt LE, CuXLP and Mimas15 platforms |
| wifiNetwork | joseph.rothery@hp.com | |
| power | UI: sathish-kumar.reddy@hp.com PE: chen-how.wong@hp.com smgr_power: vaibhav.malik@hp.com | |
| uuidInfo (deprecated) | pradeep.potturi@hp.com | Deprecated since Dec 2022 |
| lifetimeCountersSnapshot | rodney.tay@hp.com, kiran.kum.p-n@hp.com | |
| wifiNetwork | joseph.rothery@hp.com | |
| wifiSetup | joseph.rothery@hp.com | |
| engineStats | PUN, YONG SENG (yong.seng.pun@hp.com) Chia, Chun Choon (chun.choon.chia@hp.com) Kedar, Ajay (ajay.kedar@hp.com) | |
| rtp | Subhash Pulikkara Veedu | |
| job | ajay.kedar@hp.com, Smita Devi | |
| iotOnboarding | archana.kode@hp.com | |
| frontPanelFlow | joseph.rothery@hp.com | |
| healthTracker (deprecated) | ansut@hp.com | Deprecated since Dec 2022 |
| calibrationData (deprecated) | ansut@hp.com | Deprecated since Dec 2022 |

Apollo/Horizon Product Line (JIRA SMBFW) (TPM: shreevathsa.jayadeva@hp.com)

| EventCategory | Primary/Secondary owners | Scope/Platform inclusions |
|---|---|---|
| fwUpdate | sreenivasa.chakavarthy@hp.com | |
| supply | kaustav.paul@hp.com | |
| rtp | sreenivasa.chakavarthy@hp.com | |
| lifetimeCounterSnapshot | mohammed.waseem@hp.com | |

Jedi Product Line (JIRA JOLT) (TPM: nagaraj.padshetty@hp.com)

| EventCategory | Primary/Secondary owners | Scope/Platform inclusions |
|---|---|---|
| supply | ashok.kopparthi@hp.com vineetha.james@hp.com | |

Dune Product Line (JIRA DUNE) (TPM: kanghoon.lee@hp.com)

| EventCategory | Primary/Secondary owners | Scope/Platform inclusions |
|---|---|---|
| fwUpdate | Fidel Angel Vanegas Stephen Schwarz | |
| supply | Suma Byrappa Anukeerthana P | |
| rtp | Subhash Pulikkara Veedu | |
| lifetimeCounterSnapshot | Monica Pujol Edward Peralta | |
| job | Monica Pujol Edward Peralta | |
| info, warning, error system events | KRISHNA JHA | |
| wifiSetup, wifiNetwork , frontPanelFlow | Joseph Rothery | |
| iotOnboarding | Sagir Sarkar Rahman Krishnaswamy R | |

Ares Product Line (JIRA Low Ink Firmware) (TPM: saurabh.srivastava2@hp.com)

| EventCategory | Primary/Secondary owners | Scope/Platform inclusions | Specific to Dragonfly |
|---|---|---|---|
| fwUpdate | Greg Hargis Kathy Smektala | | |
| supply | Rodney Tay Kiran Kumar Palyam Nagendra | | |
| rtp | Subhash Pulikkara Veedu Abdul Waseem Mohammed | | |
| lifetimeCounterSnapshot | Rodney Tay Mohd Waris Ansari | | |
| job | Saurabh Srivastava Shakti Saxena | | |
| wifiSetup, wifiNetwork , frontPanelFlow | Joseph Rothery u Teik Hor Soon | | |
| iotOnboarding | Sreenivasa Chakravarthy G | unknown | |
| systemEvent (info, warning, error) | Shweta Saha | | |