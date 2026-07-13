<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CRIMSON MANOR: CASE FILE #404</title>
    <style>
        :root {
            --neon-red: #ff003c;
            --dark-bg: #030305;
            --terminal-green: #39ff14;
            --text-gray: #9ba0b0;
            --gold-accent: #c99738;
        }

        body {
            background-color: var(--dark-bg);
            color: var(--text-gray);
            font-family: 'Courier New', Courier, monospace;
            margin: 0;
            padding: 0;
            overflow-x: hidden;
            background-image: radial-gradient(rgba(217, 30, 30, 0.05) 15%, transparent 16%);
            background-size: 6px 6px;
        }

        /* Scanline overlay for that gritty, retro CRT investigation look */
        body::before {
            content: " ";
            display: block;
            position: fixed;
            top: 0; left: 0; bottom: 0; right: 0;
            background: linear-gradient(rgba(18, 16, 16, 0) 50%, rgba(0, 0, 0, 0.35) 50%), linear-gradient(90deg, rgba(255, 0, 0, 0.04), rgba(0, 255, 0, 0.01), rgba(0, 0, 255, 0.04));
            z-index: 99999;
            background-size: 100% 4px, 4px 100%;
            pointer-events: none;
        }

        .wrapper {
            max-width: 900px;
            margin: 40px auto;
            padding: 40px;
            background: rgba(10, 10, 14, 0.98);
            border: 1px solid #222230;
            box-shadow: 0 0 50px rgba(0, 0, 0, 0.9), inset 0 0 30px rgba(255, 0, 60, 0.03);
            position: relative;
        }

        .wrapper::after {
            content: '';
            position: absolute;
            top: 0; left: 0; width: 100%; height: 3px;
            background: linear-gradient(90deg, transparent, var(--neon-red), transparent);
            box-shadow: 0 0 15px var(--neon-red);
        }

        header h1 {
            color: #fff;
            text-align: center;
            font-size: 2.4rem;
            letter-spacing: 6px;
            text-shadow: 0 0 12px var(--neon-red);
            margin-bottom: 5px;
        }

        .case-status {
            text-align: center;
            color: var(--gold-accent);
            font-size: 0.85rem;
            text-transform: uppercase;
            letter-spacing: 3px;
            margin-bottom: 35px;
            animation: blink 2.5s infinite;
        }

        /* Noir Atmospheric Image Header */
        .scenery-banner {
            width: 100%;
            height: auto;
            border: 1px solid #2d2d3f;
            margin-bottom: 40px;
            box-shadow: 0 0 25px rgba(0, 0, 0, 0.7);
            display: block;
        }

        /* Detective Dossier Split layout */
        .dossier {
            display: grid;
            grid-template-columns: 220px 1fr;
            gap: 30px;
            background: #07070a;
            border: 1px solid #1a1a26;
            padding: 25px;
            margin-bottom: 40px;
        }

        .detective-avatar {
            width: 100%;
            height: 240px;
            border: 1px solid #333344;
            background: #0c0c12;
            position: relative;
        }

        .dossier-details h3 {
            color: #fff;
            margin-top: 0;
            border-bottom: 1px solid #2a2a3a;
            padding-bottom: 8px;
            letter-spacing: 2px;
            font-size: 1.2rem;
        }

        .dossier-details p {
            font-size: 0.95rem;
            color: #8c91a0;
            line-height: 1.6;
        }

        .dossier-details strong {
            color: var(--gold-accent);
        }

        /* Narrative & Case Files */
        .case-file-content {
            border-left: 2px solid var(--neon-red);
            padding-left: 25px;
            margin-bottom: 45px;
        }

        .case-file-content p {
            margin-bottom: 22px;
            text-align: justify;
            line-height: 1.7;
            font-size: 1rem;
        }

        .clue-highlight {
            color: #fff;
            background: rgba(255, 0, 60, 0.08);
            padding: 2px 6px;
            border-bottom: 1px dashed var(--neon-red);
        }

        /* Interactive Interrogation Zone */
        .interrogation-zone {
            background: #060609;
            border: 1px solid #1c1c28;
            padding: 35px;
            text-align: center;
            position: relative;
        }

        .interrogation-zone h2 {
            color: #fff;
            font-size: 1.5rem;
            margin-top: 0;
            letter-spacing: 3px;
        }

        select {
            background: #0d0d14;
            color: #fff;
            border: 1px solid #333346;
            padding: 12px 20px;
            font-family: inherit;
            width: 65%;
            margin-bottom: 25px;
            outline: none;
            letter-spacing: 1px;
        }

        select:focus {
            border-color: var(--neon-red);
            box-shadow: 0 0 10px rgba(255, 0, 60, 0.2);
        }

        .btn-accuse {
            background: var(--neon-red);
            color: white;
            border: none;
            padding: 14px 35px;
            font-family: inherit;
            font-weight: bold;
            text-transform: uppercase;
            cursor: pointer;
            letter-spacing: 2px;
            box-shadow: 0 0 15px rgba(255, 0, 60, 0.3);
            transition: all 0.2s ease;
        }

        .btn-accuse:hover {
            background: #d00030;
            box-shadow: 0 0 25px var(--neon-red);
        }

        .log-output {
            margin-top: 25px;
            font-weight: bold;
            min-height: 24px;
            letter-spacing: 1px;
        }

        /* The Final Crimson Horror Breakdown */
        .horror-reveal {
            display: none;
            margin-top: 45px;
            padding: 35px;
            background: #000;
            border: 1px solid var(--neon-red);
            box-shadow: 0 0 50px rgba(255, 0, 0, 0.3);
            animation: cameraFlash 0.4s ease-out;
        }

        .horror-title {
            color: var(--neon-red) !important;
            font-size: 2.2rem;
            text-shadow: 0 0 15px #ff0000;
            text-align: center;
            letter-spacing: 5px;
        }

        .horror-image-container {
            width: 100%;
            max-width: 450px;
            margin: 30px auto;
            border: 1px solid #330005;
            background: #020202;
        }

        @keyframes blink {
            0%, 100% { opacity: 1; }
            50% { opacity: 0.4; }
        }

        @keyframes cameraFlash {
            0% { background: #50000a; }
            100% { background: #000; }
        }
    </style>
</head>
<body>

    <div class="wrapper">
        <header>
            <h1>UNSOLVED LOG: CRIMSON MANOR</h1>
            <div class="case-status">// TAP ANYWHERE TO INTERACT AND INITIALIZE AUDIO DATA //</div>
        </header>

        <!-- Dynamic Cinematic Visual Asset Placement -->
        <img src="watermarked_img_2097412931571847981.png" alt="Detective Office Landscape" class="scenery-banner">

        <!-- Detective Dossier Segment -->
        <div class="dossier">
            <div class="detective-avatar">
                <!-- High Contrast Minimalist Vector Face Art -->
                <svg viewBox="0 0 100 100" width="100%" height="100%">
                    <rect width="100" height="100" fill="#050508"/>
                    <path d="M15 45 L85 45 L71 23 L29 23 Z" fill="#12121c"/>
                    <ellipse cx="50" cy="46" rx="42" ry="3.5" fill="#222232"/>
                    <path d="M31 46 Q31 76 50 84 Q69 76 69 46 Z" fill="#323244"/>
                    <path d="M31 46 Q31 76 50 84 L50 46 Z" fill="#242434"/>
                    <path d="M18 95 L35 73 L50 85 L65 73 L82 95 Z" fill="#161622"/>
                    <path d="M18 95 L28 70 L50 85 Z" fill="#0e0e16"/>
                    <circle cx="48" cy="67" r="1.3" fill="#ff4400" style="animation: blink 1.5s infinite;"/>
                    <path d="M48 67 Q43 58 46 50" stroke="rgba(255,255,255,0.12)" stroke-width="0.5" fill="none"/>
                </svg>
            </div>
            <div class="dossier-details">
                <h3>DETECTIVE PROFILE</h3>
                <p><strong>OPERATIVE:</strong> Inspector Silas Vance</p>
                <p><strong>DEPARTMENT:</strong> Occult & Cold Case Division</p>
                <p><strong>PROFILE:</strong> Vance tracks anomalies standard tactical units flatly ignore. Operating out of the fog-drenched streets of New Arkham, his structural evaluation methodologies are clinical, hyper-observant, and entirely unyielding. He treats a locked room crime scene not as a geometric puzzle, but as a dynamic predator's cage waiting to slam shut on the uninitiated.</p>
            </div>
        </div>

        <!-- Narrative Base Content -->
        <div class="case-file-content">
            <p><strong>THE CASE:</strong> Lord Adrian Blackwood was discovered dead inside his high-security fortress study at precisely midnight. The heavy solid oak entry door assemblies were bolted firmly from the inside with thick iron structural sliding bars. The exterior windows were completely welded shut for winter preservation. There were absolutely no structural anomalies or secret panels. Yet, he sat completely lifeless at his desk, his jaw frozen in a grimace of absolute, unnatural horror.</p>
            
            <p><strong>THE TIMELINE & ALIBIS:</strong> Four distinct entities occupied the manor grounds during the blinding mountain snowstorm.
            <br>1. <span class="clue-highlight">Lady Eleanor (The Wife)</span>: Confirms she spent the evening down in the highly insulated greenhouse conservatory, cultivating her collection of nocturnal orchids.
            <br>2. <span class="clue-highlight">Arthur (The Butler)</span>: Asserts he remained static inside the butler's pantry polishing the historical silver dining sets.
            <br>3. <span class="clue-highlight">Dr. Harrison (The Physician)</span>: Asserts he lapsed into deep sleep in the distant east wing guest suite immediately following Lord Blackwood's evening medical evaluation checkup.
            <br>4. <span class="clue-highlight">Julian (The Estranged Son)</span>: Claims he was deep in the far archives translating an ancient family manuscript regarding territorial claims.</p>

            <p><strong>THE TWISTS:</strong> Vance systematically mapped the floor plan and isolated severe chronological paradoxes. Lord Blackwood's evening tea cup sat completely full—untouched. However, the <span class="clue-highlight">antique grandfather clock</span> sitting in the corner, non-functional for half a century, was mysteriously ticking loud, rapid, and heavy. Most critically, an open fountain pen lay dropped on the desk surface adjacent to an unblemished sheet of empty parchment paper. The room air carried a dense scent of bitter almonds—the undeniable indicator of immediate cyanide ingestion.</p>

            <p>Julian immediately noted that his father’s fingertips were entirely pristine, lacking any signature ink deposits, indicating he had never actually drafted a letter. Dr. Harrison supplemented that the toxin was explicitly configured as a concentrated contact poison. Arthur the butler frantically whispered that Lord Blackwood always recorded his journal entries exactly five minutes prior to midnight. Lady Eleanor simply wept bitterly, declaring the old family curse active.</p>

            <p>Vance bolted the mansion gates. The perpetrator believed the sealed interior layout provided perfect immunity. But they miscalculated a chronological engine trap. The grandfather clock was not running on internal gears; it was housing a modern, hidden spring assembly calibrated to trigger precisely at midnight, driving the heavy interior iron door bolts forward using a hidden system of tension wire cables embedded inside the hollow partition walls. The door was locked *after* the death occurred, completely manufacturing the locked-room anomaly.</p>
        </div>

        <!-- Interactive Form Section -->
        <div class="interrogation-zone">
            <h2>SUBMIT CRIMINAL CHARGE</h2>
            <p>Which individual manipulated the mechanical clock array to lock the perimeter after the execution?</p>
            
            <select id="suspectCtrl">
                <option value="">-- SELECT TARGET SUSPECT --</option>
                <option value="eleanor">Lady Eleanor</option>
                <option value="harrison">Dr. Harrison</option>
                <option value="julian">Julian Blackwood</option>
                <option value="arthur">Arthur the Butler</option>
            </select>
            <br>
            <button class="btn-accuse" onclick="processAccusation()">Execute Arrest Warrant</button>

            <div class="log-output" id="logOutput"></div>
        </div>

        <!-- Horror Reveal Panel Element -->
        <div class="horror-reveal" id="horrorReveal">
            <h2 class="horror-title">ARCHIVE RECORD DETONATION</h2>
            <p id="finalStoryText"></p>
            
            <div class="horror-image-container">
                <!-- Demonic Entity Aesthetic High Contrast Graphic Vector -->
                <svg viewBox="0 0 200 200" width="100%" height="100%">
                    <path d="M 0,0 L 200,200 M 200,0 L 0,200" stroke="#1c0205" stroke-width="4"/>
                    <path d="M60 200 Q40 120 70 85 Q60 55 80 35 Q100 15 120 35 Q140 55 130 85 Q160 120 140 200 Z" fill="#080202"/>
                    <path d="M75 75 Q100 45 125 75 Q100 115 75 75 Z" fill="#150406"/>
                    <circle cx="88" cy="72" r="4.5" fill="#ff002c" filter="drop-shadow(0px 0px 6px #ff0000)"/>
                    <circle cx="112" cy="72" r="4.5" fill="#ff002c" filter="drop-shadow(0px 0px 6px #ff0000)"/>
                    <path d="M 82,92 Q 100,112 118,92 Q 100,99 82,92" fill="#000" stroke="#ff002c" stroke-width="2"/>
                    <path d="M15 15 L25 35 L20 45 Z M185 35 L175 65 L180 55 Z" fill="#2a0005"/>
                    <rect x="0" y="130" width="200" height="6" fill="rgba(255,0,50,0.2)"/>
                </svg>
            </div>
            <p style="color:#444; font-size:0.75rem; text-align:center; letter-spacing: 2px;">// MANOR ARCHIVE SYSTEM BREACHED // UNKNOWABLE ENTITY DETECTED //</p>
        </div>
    </div>

    <script>
        let strikeCount = 0;
        
        // Advanced Web Audio Synthesis Nodes
        let audioCtx = null;
        let subDrone = null;
        let harmonicClash1 = null;
        let harmonicClash2 = null;
        let modularLfo = null;
        let masterFilter = null;
        let backgroundEngineActive = false;

        // Bypasses browser autoplay restrictions via tactical global initialization listeners
        window.addEventListener('DOMContentLoaded', () => {
            const bootAudioSystem = () => {
                if (!backgroundEngineActive) {
                    initHorrorAudioEngine();
                }
                document.removeEventListener('click', bootAudioSystem);
                document.removeEventListener('keydown', bootAudioSystem);
            };
            document.addEventListener('click', bootAudioSystem);
            document.addEventListener('keydown', bootAudioSystem);
        });

        function initHorrorAudioEngine() {
            try {
                audioCtx = new (window.AudioContext || window.webkitAudioContext)();
                
                // Muffled Lowpass filters simulate structural isolation and deep dread
                masterFilter = audioCtx.createBiquadFilter();
                masterFilter.type = 'lowpass';
                masterFilter.frequency.setValueAtTime(180, audioCtx.currentTime);

                // 1. Deep Sub-Bass Ground Drone (Structural Resonance Anomaly)
                subDrone = audioCtx.createOscillator();
                subDrone.type = 'sawtooth';
                subDrone.frequency.setValueAtTime(43.65, audioCtx.currentTime); // Violent F1 frequency
                
                let subGain = audioCtx.createGain();
                subGain.gain.setValueAtTime(0.28, audioCtx.currentTime);
                subDrone.connect(subGain);
                subGain.connect(masterFilter);

                // 2. High Frequency Jarring Clashing Pair (Simulates acoustic beating/anxiety)
                harmonicClash1 = audioCtx.createOscillator();
                harmonicClash1.type = 'sawtooth';
                harmonicClash1.frequency.setValueAtTime(130.81, audioCtx.currentTime); // C3 frequency
                
                harmonicClash2 = audioCtx.createOscillator();
                harmonicClash2.type = 'square';
                harmonicClash2.frequency.setValueAtTime(134.50, audioCtx.currentTime); // Sharp dissonant micro-interval
                
                let tensionGain = audioCtx.createGain();
                tensionGain.gain.setValueAtTime(0.06, audioCtx.currentTime);
                
                harmonicClash1.connect(tensionGain);
                harmonicClash2.connect(tensionGain);
                tensionGain.connect(masterFilter);

                // 3. Dynamic Low Frequency Oscillator (LFO - Simulates labored breathing cycles)
                modularLfo = audioCtx.createOscillator();
                modularLfo.type = 'sine';
                modularLfo.frequency.setValueAtTime(0.22, audioCtx.currentTime); // Extremely slow wave cycles
                
                let lfoDepth = audioCtx.createGain();
                lfoDepth.gain.setValueAtTime(95, audioCtx.currentTime); // Sweeps cutoff filter point
                
                modularLfo.connect(lfoDepth);
                lfoDepth.connect(masterFilter.frequency);

                // Master output attenuation routing
                let finalOutGain = audioCtx.createGain();
                finalOutGain.gain.setValueAtTime(0.90, audioCtx.currentTime);
                masterFilter.connect(finalOutGain);
                finalOutGain.connect(audioCtx.destination);

                // Initialize all synthetic audio streams synchronously
                subDrone.start();
                harmonicClash1.start();
                harmonicClash2.start();
                modularLfo.start();

                document.querySelector('.case-status').innerText = "// AUDIO SURVEILLANCE FEED ACTIVE // DETECTIVE MATRIX ACTIVE //";
                backgroundEngineActive = true;

            } catch(error) {
                console.error("Web Audio deployment failed initialization:", error);
            }
        }

        function processAccusation() {
            const selectVal = document.getElementById('suspectCtrl').value;
            const output = document.getElementById('logOutput');
            const revealContainer = document.getElementById('horrorReveal');
            const finalStoryText = document.getElementById('finalStoryText');

            if (!selectVal) {
                output.innerHTML = "<span style='color:orange;'>[ERROR: SELECT VALID COMPONENT DEVIATION]</span>";
                return;
            }

            if (selectVal === "harrison") {
                output.innerHTML = "<span style='color:var(--terminal-green);'>[CASE SOLVED: ARCHIVE UNLOCKED]</span>";
                finalStoryText.innerHTML = "<strong>CRIMSON CASE STATUS: RESOLVED</strong><br><br>Dr. Harrison was the mastermind. During the evening health checkup, he painted the transparent, deadly cyanide base directly onto the grip of Lord Blackwood's favorite fountain pen. Harrison knew the Lord's absolute habit was to write in his private logs right at midnight. Harrison used his knowledge of the Manor's architectural layout to rig the old grandfather clock weights to the door bolts earlier that afternoon. When the clock struck twelve, the weight dropped, the cables pulled the heavy iron bars into place from the inside, creating a 'perfect' locked-room illusion while Harrison sat safely away in the east wing.";
                revealContainer.style.display = "block";
                revealContainer.scrollIntoView({ behavior: 'smooth' });
            } else {
                strikeCount++;
                if (strikeCount === 1) {
                    output.innerHTML = "<span style='color:var(--neon-red);'>[WARNING: MATERIAL ALIBI COHERENT. SUSPECT EXONERATED. RE-EVALUATE]</span>";
                } else {
                    output.innerHTML = "<span style='color:#ff0000; font-size:1.1rem;'>[SYSTEM CRITICAL FAILURE: DOSSIER MALICIOUS COMPROMISE]</span>";
                    
                    finalStoryText.innerHTML = "<strong>CASE STATUS: COMPROMISED</strong><br><br>Your deduction failed. The delay allowed the actual killer, <strong>Dr. Harrison</strong>, to clear his tracks and escape into the winter storm. He poisoned the fountain pen's grip during the checkup and rigged the grandfather clock to drop the door bolts exactly at midnight via dynamic internal pulley frames. Because you targeted an innocent soul, the dark curse of Crimson Manor has manifested to consume the investigation files entirely...";
                    
                    revealContainer.style.display = "block";
                    
                    // Flash screen red for dramatic layout breakdown impact
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
