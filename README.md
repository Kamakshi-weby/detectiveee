<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>THE BLACKWOOD PARADOX: CASE FILE #404</title>
    <style>
        :root {
            --neon-red: #ff003c;
            --dark-bg: #030305;
            --terminal-green: #39ff14;
            --text-gray: #9ba0b0;
            --gold-accent: #c99738;
            --deep-blood: #4a000b;
        }

        body {
            background-color: var(--dark-bg);
            color: var(--text-gray);
            font-family: 'Courier New', Courier, monospace;
            margin: 0;
            padding: 0;
            overflow-x: hidden;
            background-image: radial-gradient(rgba(217, 30, 30, 0.07) 15%, transparent 16%);
            background-size: 6px 6px;
        }

        /* Gritty CRT TV / Noir Cinema scanline emulation */
        body::before {
            content: " ";
            display: block;
            position: fixed;
            top: 0; left: 0; bottom: 0; right: 0;
            background: linear-gradient(rgba(18, 16, 16, 0) 50%, rgba(0, 0, 0, 0.4) 50%), linear-gradient(90deg, rgba(255, 0, 0, 0.05), rgba(0, 255, 0, 0.01), rgba(0, 0, 255, 0.05));
            z-index: 99999;
            background-size: 100% 4px, 4px 100%;
            pointer-events: none;
        }

        .wrapper {
            max-width: 900px;
            margin: 50px auto;
            padding: 45px;
            background: rgba(8, 8, 12, 0.98);
            border: 1px solid #1c1c28;
            box-shadow: 0 0 60px rgba(0, 0, 0, 0.95), inset 0 0 40px rgba(255, 0, 60, 0.04);
            position: relative;
        }

        .wrapper::after {
            content: '';
            position: absolute;
            top: 0; left: 0; width: 100%; height: 4px;
            background: linear-gradient(90deg, transparent, var(--neon-red), transparent);
            box-shadow: 0 0 20px var(--neon-red);
        }

        header h1 {
            color: #fff;
            text-align: center;
            font-size: 2.6rem;
            letter-spacing: 7px;
            text-shadow: 0 0 15px var(--neon-red);
            margin-bottom: 5px;
            font-weight: 900;
        }

        .case-status {
            text-align: center;
            color: var(--gold-accent);
            font-size: 0.9rem;
            text-transform: uppercase;
            letter-spacing: 4px;
            margin-bottom: 40px;
            text-shadow: 0 0 5px rgba(201, 151, 56, 0.3);
            animation: breathe 3s infinite ease-in-out;
        }

        /* Cinematic Office Banner Image */
        .scenery-banner {
            width: 100%;
            height: auto;
            border: 1px solid #222230;
            margin-bottom: 45px;
            box-shadow: 0 0 35px rgba(0, 0, 0, 0.85);
            display: block;
        }

        /* Detective Dossier Grid Layout */
        .dossier {
            display: grid;
            grid-template-columns: 220px 1fr;
            gap: 35px;
            background: #06060a;
            border: 1px solid #161622;
            padding: 30px;
            margin-bottom: 45px;
            box-shadow: inset 0 0 20px rgba(0,0,0,0.8);
        }

        .detective-avatar {
            width: 100%;
            height: 240px;
            border: 1px solid #2d2d3d;
            background: #09090f;
            position: relative;
            box-shadow: 0 0 15px rgba(0,0,0,0.6);
        }

        .dossier-details h3 {
            color: #fff;
            margin-top: 0;
            border-bottom: 1px solid #252538;
            padding-bottom: 10px;
            letter-spacing: 3px;
            font-size: 1.3rem;
            text-shadow: 0 0 5px rgba(255,255,255,0.2);
        }

        .dossier-details p {
            font-size: 0.95rem;
            color: #8c92a5;
            line-height: 1.7;
        }

        .dossier-details strong {
            color: var(--gold-accent);
            letter-spacing: 1px;
        }

        /* Narrative & Case Documentation Style */
        .case-file-content {
            border-left: 3px solid var(--neon-red);
            padding-left: 30px;
            margin-bottom: 50px;
        }

        .case-file-content p {
            margin-bottom: 25px;
            text-align: justify;
            line-height: 1.8;
            font-size: 1.05rem;
            letter-spacing: 0.5px;
        }

        .clue-highlight {
            color: #fff;
            background: rgba(255, 0, 60, 0.12);
            padding: 3px 8px;
            border-bottom: 1px dashed var(--neon-red);
            font-weight: bold;
        }

        /* Suspect Interactive Grid Layout */
        .interrogation-zone {
            background: #050508;
            border: 1px solid #141420;
            padding: 40px;
            text-align: center;
            box-shadow: inset 0 0 30px rgba(0,0,0,0.9);
        }

        .interrogation-zone h2 {
            color: #fff;
            font-size: 1.6rem;
            margin-top: 0;
            letter-spacing: 4px;
            text-shadow: 0 0 8px rgba(255,255,255,0.3);
        }

        .interrogation-zone p {
            font-size: 0.95rem;
            margin-bottom: 25px;
            color: #7b8090;
        }

        select {
            background: #0b0b12;
            color: #fff;
            border: 1px solid #2d2d3f;
            padding: 14px 25px;
            font-family: inherit;
            width: 70%;
            font-size: 1rem;
            margin-bottom: 30px;
            outline: none;
            letter-spacing: 1px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.5);
        }

        select:focus {
            border-color: var(--neon-red);
            box-shadow: 0 0 15px rgba(255, 0, 60, 0.3);
        }

        .btn-accuse {
            background: var(--neon-red);
            color: white;
            border: none;
            padding: 16px 40px;
            font-family: inherit;
            font-weight: bold;
            font-size: 1rem;
            text-transform: uppercase;
            cursor: pointer;
            letter-spacing: 2px;
            box-shadow: 0 0 20px rgba(255, 0, 60, 0.4);
            transition: all 0.2s ease-in-out;
        }

        .btn-accuse:hover {
            background: #d00030;
            box-shadow: 0 0 30px var(--neon-red);
            transform: scale(1.02);
        }

        .log-output {
            margin-top: 30px;
            font-weight: bold;
            min-height: 24px;
            letter-spacing: 1px;
            font-size: 1.1rem;
        }

        /* Horror Revelation Layout Climax */
        .horror-reveal {
            display: none;
            margin-top: 50px;
            padding: 40px;
            background: #000;
            border: 1px solid var(--neon-red);
            box-shadow: 0 0 60px rgba(255, 0, 0, 0.45);
            animation: cameraFlash 0.5s ease-out;
        }

        .horror-title {
            color: var(--neon-red) !important;
            font-size: 2.4rem;
            text-shadow: 0 0 20px #ff0000;
            text-align: center;
            letter-spacing: 6px;
            font-weight: 900;
        }

        .horror-image-container {
            width: 100%;
            max-width: 450px;
            margin: 35px auto;
            border: 1px solid #40000a;
            background: #010101;
            box-shadow: 0 0 25px rgba(255,0,0,0.1);
        }

        @keyframes breathe {
            0%, 100% { opacity: 1; transform: scale(1); }
            50% { opacity: 0.5; transform: scale(0.99); }
        }

        @keyframes blink {
            0%, 100% { opacity: 1; }
            50% { opacity: 0.2; }
        }

        @keyframes cameraFlash {
            0% { background: var(--deep-blood); filter: brightness(2); }
            100% { background: #000; filter: brightness(1); }
        }
    </style>
</head>
<body>

    <div class="wrapper">
        <header>
            <h1>THE BLACKWOOD PARADOX</h1>
            <div class="case-status" id="systemStatus">// CLICK ANYWHERE ON SCREEN TO ACTIVATE AUDIO FEED & BEGIN INVESTIGATION //</div>
        </header>

        <!-- Cinematic Noir Scene Placement (The Image Provided) -->
        <img src="watermarked_img_2097412931571847981.png" alt="Detective Silas Vance in his smoke-filled Arkham Office" class="scenery-banner">

        <!-- Detective Dossier Segment -->
        <div class="dossier">
            <div class="detective-avatar">
                <!-- High Contrast Minimalist Vector Portrait -->
                <svg viewBox="0 0 100 100" width="100%" height="100%">
                    <rect width="100" height="100" fill="#040406"/>
                    <path d="M15 45 L85 45 L71 23 L29 23 Z" fill="#10101a"/>
                    <ellipse cx="50" cy="46" rx="42" ry="3.5" fill="#1f1f2e"/>
                    <path d="M31 46 Q31 76 50 84 Q69 76 69 46 Z" fill="#2d2d3d"/>
                    <path d="M31 46 Q31 76 50 84 L50 46 Z" fill="#20202e"/>
                    <path d="M18 95 L35 73 L50 85 L65 73 L82 95 Z" fill="#14141f"/>
                    <path d="M18 95 L28 70 L50 85 Z" fill="#0b0b12"/>
                    <circle cx="48" cy="67" r="1.3" fill="#ff3300" style="animation: blink 2s infinite;"/>
                    <path d="M48 67 Q43 58 46 50" stroke="rgba(255,255,255,0.1)" stroke-width="0.5" fill="none"/>
                </svg>
            </div>
            <div class="dossier-details">
                <h3>INVESTIGATOR FILE</h3>
                <p><strong>OPERATIVE:</strong> Inspector Silas Vance</p>
                <p><strong>DIVISION:</strong> Occult Anomalies & Locked-Room Homicide</p>
                <p><strong>DOSSIER:</strong> Vance is a broken man hunting unbroken puzzles. Stationed above an occult bookstore in the shadow-drenched alleys of New Arkham, his methods are clinical, hyper-observant, and deeply cynical. He doesn't look for traditional entry points; he tracks the psychological and mechanical traps left behind by those who think they are gods. To Vance, a sealed room isn't an impossibility—it's an execution theater.</p>
            </div>
        </div>

        <!-- The Dark Detective Mystery Story -->
        <div class="case-file-content">
            <p><strong>THE CRIME:</strong> At precisely midnight, a frantic alarm tore through the isolated, blizzard-struck Crimson Manor. Lord Adrian Blackwood, an eccentric billionaire obsessed with mechanical horology and hidden systems, was found dead at his mahogany desk. The scene was an mathematical impossibility: the solid oak study doors were bolted from the inside with heavy structural iron bars. The massive gothic windows were entirely welded shut for the winter storms. There were no hidden passages, trick panels, or architectural structural gaps. Yet, Blackwood sat dead, his eyes wide, frozen in a silent scream of absolute, pure terror.</p>
            
            <p><strong>THE ALIBIS:</strong> Four individuals trapped inside the manor by the snowstorm have become the primary targets of Vance's cold gaze:
            <br>1. <span class="clue-highlight">Lady Eleanor (The Devastated Wife)</span>: Claims she was spending the late hours in the highly insulated greenhouse conservatory, tending to her rare, nocturnal predatory orchids.
            <br>2. <span class="clue-highlight">Arthur (The Stoic Butler)</span>: Asserts he never left the basement silver pantry, methodically polishing the family's heavy heirloom sterling dining utensils.
            <br>3. <span class="clue-highlight">Dr. Harrison (The Family Physician)</span>: Insists he was completely unconscious in the east wing guest suite after completing Lord Blackwood's scheduled evening medical evaluation checkup.
            <br>4. <span class="clue-highlight">Julian (The Disinherited Son)</span>: Claims he was locked away in the far mansion library translating an ancient medieval manuscript regarding ancestral land boundaries.</p>

            <p><strong>THE ANOMALIES:</strong> As Vance surveyed the suffocating room, the contradictions shattered the suspects' constructed realities. Lord Blackwood’s midnight tea cup sat completely full—untouched. Mysteriously, a massive <span class="clue-highlight">antique grandfather clock</span> in the corner, mechanical gears broken and dead for over fifty years, was suddenly ticking with a loud, fast, hyper-frenetic rhythm. Most damningly, an open fountain pen lay dropped on the floor near an unblemished sheet of empty paper. The air reeked heavily of bitter almonds—the undeniable calling card of lethal, swift-acting cyanide poisoning.</p>

            <p>Julian quickly sneered that his father's hands were perfectly clean, lacking any ink stains, proving he never wrote a word. Dr. Harrison added that the heavy toxicity was a concentrated contact poison meant to kill within seconds of touch. Arthur whispered nervously that the Lord’s unyielding ritual was to pen his secret journal entries exactly five minutes before midnight. Lady Eleanor collapsed in tears, claiming a demonic entity had claimed her husband's soul.</p>

            <p>Vance quietly locked the front gates. The killer believed the perfectly sealed room exonerated them. But they missed a fatal engineering oversight. The grandfather clock was not ticking due to historic gears—it housed a modern, hidden tension-spring rig timed to release exactly at midnight, throwing the heavy interior iron sliding bolts forward through a system of hidden pulley lines woven directly inside the hollow wooden lath walls. The room was locked *after* the murder took place, entirely staging the locked-room illusion.</p>
        </div>

        <!-- Interrogation Interacting Space -->
        <div class="interrogation-zone">
            <h2>DEDUCE THE KILLER</h2>
            <p>Analyze the mechanical setup, the alibis, and the physical anomalies. Who rigged the room to execute the perfect crime?</p>
            
            <select id="suspectCtrl">
                <option value="">-- ACCUSE SUSPECT --</option>
                <option value="eleanor">Lady Eleanor (The Orchid Enthusiast)</option>
                <option value="arthur">Arthur (The Quiet Butler)</option>
                <option value="harrison">Dr. Harrison (The Attending Physician)</option>
                <option value="julian">Julian Blackwood (The Estranged Heir)</option>
            </select>
            <br>
            <button class="btn-accuse" onclick="processAccusation()">File Final Charge</button>

            <div class="log-output" id="logOutput"></div>
        </div>

        <!-- Master Climactic Horror Reveal Element -->
        <div class="horror-reveal" id="horrorReveal">
            <h2 class="horror-title">THE CASE IS SEALED</h2>
            <p id="finalStoryText"></p>
            
            <div class="horror-image-container">
                <!-- Distorted Abstract Horror entity Vector Image -->
                <svg viewBox="0 0 200 200" width="100%" height="100%">
                    <path d="M 0,0 L 200,200 M 200,0 L 0,200" stroke="#210205" stroke-width="4"/>
                    <path d="M60 200 Q40 120 70 85 Q60 55 80 35 Q100 15 120 35 Q140 55 130 85 Q160 120 140 200 Z" fill="#0a0303"/>
                    <path d="M75 75 Q100 45 125 75 Q100 115 75 75 Z" fill="#1c0508"/>
                    <circle cx="88" cy="72" r="4.5" fill="#ff002c" filter="drop-shadow(0px 0px 6px #ff0000)"/>
                    <circle cx="112" cy="72" r="4.5" fill="#ff002c" filter="drop-shadow(0px 0px 6px #ff0000)"/>
                    <path d="M 82,92 Q 100,112 118,92 Q 100,99 82,92" fill="#000" stroke="#ff002c" stroke-width="2"/>
                    <path d="M15 15 L25 35 L20 45 Z M185 35 L175 65 L180 55 Z" fill="#360007"/>
                    <rect x="0" y="130" width="200" height="6" fill="rgba(255,0,50,0.25)"/>
                </svg>
            </div>
            <p style="color:#555; font-size:0.75rem; text-align:center; letter-spacing: 3px;">// SYSTEM ERROR // MEMORY BANK COMPROMISED // ENTITY CORRUPTION DETECTED //</p>
        </div>
    </div>

    <script>
        let strikeCount = 0;
        
        // Cinematic Web Audio Synth Architecture 
        let audioCtx = null;
        let lowDrone = null;
        let secondaryDrone = null;
        let screechNode1 = null;
        let screechNode2 = null;
        let heartRateLfo = null;
        let masterLowpass = null;
        let audioIsRunning = false;

        // Interactive trigger to handle modern browser autoplay security policies seamlessly
        window.addEventListener('DOMContentLoaded', () => {
            const engageCinematicAudio = () => {
                if (!audioIsRunning) {
                    igniteHorrorSoundscape();
                }
                document.removeEventListener('click', engageCinematicAudio);
                document.removeEventListener('keydown', engageCinematicAudio);
            };
            document.addEventListener('click', engageCinematicAudio);
            document.addEventListener('keydown', engageCinematicAudio);
        });

        function igniteHorrorSoundscape() {
            try {
                audioCtx = new (window.AudioContext || window.webkitAudioContext)();
                
                // Lowpass filter isolates high frequencies to build heavy, suffocating theater suspense
                masterLowpass = audioCtx.createBiquadFilter();
                masterLowpass.type = 'lowpass';
                masterLowpass.frequency.setValueAtTime(160, audioCtx.currentTime);

                // 1. Cinematic Deep Sub-Bass Ground Drone (The structural "manor hum")
                lowDrone = audioCtx.createOscillator();
                lowDrone.type = 'sawtooth';
                lowDrone.frequency.setValueAtTime(41.20, audioCtx.currentTime); // Low E1 frequency
                
                let lowDroneGain = audioCtx.createGain();
                lowDroneGain.gain.setValueAtTime(0.35, audioCtx.currentTime);
                lowDrone.connect(lowDroneGain);
                lowDroneGain.connect(masterLowpass);

                // 2. Desolating Mid-Tone Dissonance (Warped minor-second interval clash)
                secondaryDrone = audioCtx.createOscillator();
                secondaryDrone.type = 'square';
                secondaryDrone.frequency.setValueAtTime(82.41, audioCtx.currentTime); // E2 baseline
                
                let secondaryGain = audioCtx.createGain();
                secondaryGain.gain.setValueAtTime(0.12, audioCtx.currentTime);
                secondaryDrone.connect(secondaryGain);
                secondaryGain.connect(masterLowpass);

                // 3. Cinematic "Screeching Tension" Beating Nodes (High strings/metallic anxiety simulation)
                screechNode1 = audioCtx.createOscillator();
                screechNode1.type = 'sawtooth';
                screechNode1.frequency.setValueAtTime(120.00, audioCtx.currentTime);
                
                screechNode2 = audioCtx.createOscillator();
                screechNode2.type = 'square';
                screechNode2.frequency.setValueAtTime(123.50, audioCtx.currentTime); // Microtonal pitch clash causing structural auditory beating
                
                let tensionGain = audioCtx.createGain();
                tensionGain.gain.setValueAtTime(0.06, audioCtx.currentTime);
                screechNode1.connect(tensionGain);
                screechNode2.connect(tensionGain);
                tensionGain.connect(masterLowpass);

                // 4. Heartbeat/Pulsing LFO Filter Modulation (Gives the sound a slow, terrifying breathing movement)
                heartRateLfo = audioCtx.createOscillator();
                heartRateLfo.type = 'sine';
                heartRateLfo.frequency.setValueAtTime(0.20, audioCtx.currentTime); // Slow, deliberate wave cycles (5 seconds)
                
                let lfoDepth = audioCtx.createGain();
                lfoDepth.gain.setValueAtTime(85, audioCtx.currentTime); // Sweeps cutoff frequency boundlessly
                
                heartRateLfo.connect(lfoDepth);
                lfoDepth.connect(masterLowpass.frequency);

                // Master Output Gain Attenuation
                let masterVolume = audioCtx.createGain();
                masterVolume.gain.setValueAtTime(0.95, audioCtx.currentTime);
                masterLowpass.connect(masterVolume);
                masterVolume.connect(audioCtx.destination);

                // Start all cinematic streams simultaneously
                lowDrone.start();
                secondaryDrone.start();
                screechNode1.start();
                screechNode2.start();
                heartRateLfo.start();

                document.getElementById('systemStatus').innerText = "// CINEMATIC AUDIO FEED ESTABLISHED // DETECTIVE MATRIX ACTIVE //";
                audioIsRunning = true;

            } catch(err) {
                console.error("Web Audio Framework failed initialization:", err);
            }
        }

        function processAccusation() {
            const selectVal = document.getElementById('suspectCtrl').value;
            const output = document.getElementById('logOutput');
            const revealContainer = document.getElementById('horrorReveal');
            const finalStoryText = document.getElementById('finalStoryText');

            if (!selectVal) {
                output.innerHTML = "<span style='color:orange;'>[SYSTEM ERROR: SELECT RELEVANT TARGET DETECTED]</span>";
                return;
            }

            // Dr. Harrison is the correct culprit based on the physiological and spatial deductions
            if (selectVal === "harrison") {
                output.innerHTML = "<span style='color:var(--terminal-green);'>[CASE RESOLVED: DOSSIER UNLOCKED]</span>";
                finalStoryText.innerHTML = "<strong>CRIMSON MANOR LOG: CLOSED BY VANCE</strong><br><br>Dr. Harrison was the mastermind behind the slaughter. Under the perfect cover of the evening health checkup, he meticulously painted an invisible, hyper-concentrated film of cyanide liquid directly onto the grip of Lord Blackwood's favorite custom fountain pen. Harrison knew the billionaire's compulsive, unyielding ritual: he always gripped that exact pen to sign his logs exactly five minutes before midnight. Harrison used his exclusive access earlier that afternoon to route the tension wire pulleys from the dead grandfather clock frame into the wall studs, connecting them to the iron bars. When the clock weight dropped at midnight, the bars slid home. Harrison was safely asleep in the East Wing when the trap snapped, leaving a completely 'impossible' locked room that his medical alibi almost covered perfectly.";
                revealContainer.style.display = "block";
                revealContainer.scrollIntoView({ behavior: 'smooth' });
            } else {
                strikeCount++;
                if (strikeCount === 1) {
                    output.innerHTML = "<span style='color:var(--neon-red);'>[WARNING: ALIBI IS VERIFIED AND SECURE. RE-EVALUATE THE FILES]</span>";
                } else {
                    output.innerHTML = "<span style='color:#ff0000; font-size:1.1rem;'>[SYSTEM CRITICAL FAILURE: INTEL BREACHED]</span>";
                    
                    finalStoryText.innerHTML = "<strong>CRIMSON MANOR LOG: COLD CASE ABANDONED</strong><br><br>Your deduction failed entirely. Your hesitation allowed the real phantom killer, <strong>Dr. Harrison</strong>, to incinerate his architectural plans and vanish into the black mountain storm. He was the one who layered the fountain pen's grip with transparent cyanide during his checkup, rigging the grandfather clock's internal dropping weights to throw the heavy iron door bolts forward from within at twelve. Because you falsely accused an innocent person, the dark entities woven into Crimson Manor's foundation have breached containment to erase the archives entirely...";
                    
                    revealContainer.style.display = "block";
                    
                    // Violent crimson background flash to signal ultimate failure
                    document.body.style.backgroundColor = "#ff0000";
                    setTimeout(() => {
                        document.body.style.backgroundColor = "var(--dark-bg)";
                    }, 150);
                    
                    revealContainer.scrollIntoView({ behavior: 'smooth' });
                }
            }
        }
    </script>
</body>
</html>
