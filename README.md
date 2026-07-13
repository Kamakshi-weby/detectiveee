<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CRIMSON MANOR: CASE FILE #404</title>
    <style>
        :root {
            --neon-red: #ff003c;
            --dark-bg: #050508;
            --terminal-green: #39ff14;
            --text-gray: #a5a5b0;
        }

        body {
            background-color: var(--dark-bg);
            color: var(--text-gray);
            font-family: 'Courier New', Courier, monospace;
            margin: 0;
            padding: 0;
            overflow-x: hidden;
            background-image: radial-gradient(rgba(15, 15, 25, 0.8) 15%, transparent 16%);
            background-size: 4px 4px;
        }

        /* Scanline effect for vintage monitor feel */
        body::before {
            content: " ";
            display: block;
            position: fixed;
            top: 0; left: 0; bottom: 0; right: 0;
            background: linear-gradient(rgba(18, 16, 16, 0) 50%, rgba(0, 0, 0, 0.25) 50%), linear-gradient(90deg, rgba(255, 0, 0, 0.06), rgba(0, 255, 0, 0.02), rgba(0, 0, 255, 0.06));
            z-index: 99999;
            background-size: 100% 3px, 3px 100%;
            pointer-events: none;
        }

        .wrapper {
            max-width: 850px;
            margin: 40px auto;
            padding: 30px;
            background: rgba(13, 13, 18, 0.95);
            border: 2px solid #1a1a24;
            box-shadow: 0 0 40px rgba(0, 0, 0, 0.8), inset 0 0 20px rgba(255, 0, 60, 0.05);
            position: relative;
        }

        .wrapper::after {
            content: '';
            position: absolute;
            top: 0; left: 0; width: 100%; height: 4px;
            background: var(--neon-red);
            box-shadow: 0 0 15px var(--neon-red);
        }

        header h1 {
            color: #fff;
            text-align: center;
            font-size: 2.2rem;
            letter-spacing: 4px;
            text-shadow: 0 0 10px var(--neon-red);
            margin-bottom: 5px;
        }

        .case-status {
            text-align: center;
            color: var(--neon-red);
            font-size: 0.9rem;
            text-transform: uppercase;
            letter-spacing: 2px;
            margin-bottom: 30px;
            animation: blink 1.5s infinite;
        }

        /* Audio Engine Bar */
        .audio-bar {
            background: #111116;
            border: 1px dashed #333;
            padding: 15px;
            text-align: center;
            margin-bottom: 40px;
        }

        .btn-audio {
            background: transparent;
            color: var(--neon-red);
            border: 1px solid var(--neon-red);
            padding: 10px 25px;
            font-family: inherit;
            font-weight: bold;
            cursor: pointer;
            text-transform: uppercase;
            box-shadow: 0 0 10px rgba(255, 0, 60, 0.2);
            transition: all 0.3s ease;
        }

        .btn-audio:hover {
            background: var(--neon-red);
            color: #fff;
            box-shadow: 0 0 20px var(--neon-red);
        }

        /* Detective Dossier */
        .dossier {
            display: grid;
            grid-template-columns: 200px 1fr;
            gap: 25px;
            background: #09090d;
            border: 1px solid #222;
            padding: 20px;
            margin-bottom: 40px;
        }

        .detective-avatar {
            width: 100%;
            height: 220px;
            border: 1px solid #444;
            background: #111;
            position: relative;
            box-shadow: 0 0 15px rgba(0,0,0,0.5);
        }

        .dossier-details h3 {
            color: #fff;
            margin-top: 0;
            border-bottom: 1px solid #333;
            padding-bottom: 8px;
            letter-spacing: 1px;
        }

        .dossier-details p {
            font-size: 0.95rem;
            color: #8e8e9c;
        }

        /* Narrative */
        .case-file-content {
            border-left: 3px solid #333;
            padding-left: 20px;
            margin-bottom: 40px;
        }

        .case-file-content p {
            margin-bottom: 20px;
            text-align: justify;
        }

        .clue-highlight {
            color: #fff;
            background: rgba(255, 255, 255, 0.05);
            padding: 2px 6px;
            border-bottom: 1px dotted var(--neon-red);
        }

        /* Interactive Zone */
        .interrogation-zone {
            background: #09090d;
            border: 1px solid #222;
            padding: 30px;
            text-align: center;
        }

        .interrogation-zone h2 {
            color: #fff;
            font-size: 1.4rem;
            margin-top: 0;
            letter-spacing: 2px;
        }

        select {
            background: #121218;
            color: #fff;
            border: 1px solid #444;
            padding: 12px 20px;
            font-family: inherit;
            width: 60%;
            margin-bottom: 20px;
            outline: none;
        }

        select:focus {
            border-color: var(--neon-red);
        }

        .btn-accuse {
            background: #ff003c;
            color: white;
            border: none;
            padding: 12px 30px;
            font-family: inherit;
            font-weight: bold;
            text-transform: uppercase;
            cursor: pointer;
            letter-spacing: 1px;
        }

        .btn-accuse:hover {
            background: #d00030;
        }

        .log-output {
            margin-top: 20px;
            font-weight: bold;
            min-height: 24px;
        }

        /* The Final Horror Reveal */
        .horror-reveal {
            display: none;
            margin-top: 40px;
            padding: 30px;
            background: #000;
            border: 2px solid var(--neon-red);
            box-shadow: 0 0 40px rgba(255,0,0,0.4);
            animation: cameraFlash 0.5s ease-out;
        }

        .horror-title {
            color: var(--neon-red) !important;
            font-size: 2rem;
            text-shadow: 0 0 10px #ff0000;
        }

        .horror-image-container {
            width: 100%;
            max-width: 450px;
            margin: 25px auto;
            border: 2px solid #222;
            background: #050505;
        }

        @keyframes blink {
            0%, 100% { opacity: 1; }
            50% { opacity: 0.3; }
        }

        @keyframes cameraFlash {
            0% { background: #fff; }
            100% { background: #000; }
        }
    </style>
</head>
<body>

    <div class="wrapper">
        <header>
            <h1>UNSOLVED LOG: CRIMSON MANOR</h1>
            <div class="case-status">// AMBIENT ENGINE IDLE //</div>
        </header>

        <!-- Dynamic Ambient Audio Engine -->
        <div class="audio-bar">
            <button class="btn-audio" onclick="toggleAtmosphere()" id="audioBtn">Initiate Eerie Audio Engine</button>
            <p style="font-size:0.75rem; color:#555; margin-top:8px; margin-bottom:0;">Uses built-in synthesizer framework. No downloads required.</p>
        </div>

        <!-- Detective Profile Section with Inline Vector Portrait -->
        <div class="dossier">
            <div class="detective-avatar">
                <!-- Cool stylistic Vector Art of Detective Vance -->
                <svg viewBox="0 0 100 100" width="100%" height="100%" style="background:#111;">
                    <rect width="100" height="100" fill="#08080c"/>
                    <!-- Hat Shadow -->
                    <path d="M15 45 L85 45 L70 25 L30 25 Z" fill="#181822"/>
                    <!-- Hat Brim -->
                    <ellipse cx="50" cy="46" rx="40" ry="4" fill="#252535"/>
                    <!-- Face Silhouette -->
                    <path d="M32 46 Q32 75 50 82 Q68 75 68 46 Z" fill="#3a3a4c"/>
                    <!-- Shadow on face -->
                    <path d="M32 46 Q32 75 50 82 L50 46 Z" fill="#2c2c3a"/>
                    <!-- Collar & Coat -->
                    <path d="M20 95 L35 75 L50 85 L65 75 L80 95 Z" fill="#1c1c28"/>
                    <path d="M20 95 L30 72 L50 85 Z" fill="#12121d"/>
                    <!-- Glowing Cigar Ember -->
                    <circle cx="48" cy="68" r="1.5" fill="#ff5500" style="animation: blink 2s infinite;"/>
                    <path d="M48 68 Q44 60 46 52" stroke="rgba(255,255,255,0.15)" stroke-width="0.5" fill="none"/>
                </svg>
            </div>
            <div class="dossier-details">
                <h3>DETECTIVE DOSSIER</h3>
                <p><strong>OPERATIVE:</strong> Inspector Silas Vance</p>
                <p><strong>DEPARTMENT:</strong> Occult & Cold Case Division</p>
                <p><strong>PROFILE:</strong> Vance is an investigator who tracks anomalies standard units ignore. Operating out of the smoke-filled streets of New Arkham, his methods are clinical, unyielding, and hyper-observant. He views every crime scene not as a puzzle, but as a dynamic trap waiting to snap shut on the careless.</p>
            </div>
        </div>

        <!-- Twisted Story -->
        <div class="case-file-content">
            <p><strong>THE CASE:</strong> Lord Adrian Blackwood was discovered dead inside his high-security study at exactly midnight. The heavy oak doors were bolted firmly from the inside with iron bars. The windows were completely welded shut for winter. There were absolutely no secret panels. Yet, he sat lifeless at his desk, his face frozen in a look of sheer, absolute terror.</p>
            
            <p><strong>THE TIMELINE & ALIBIS:</strong> Four individuals occupied the manor during the snowstorm.
            <br>1. <span class="clue-highlight">Lady Eleanor (The Wife)</span>: Claims she spent the evening down in the insulated conservatory, cultivating her rare nocturnal orchids.
            <br>2. <span class="clue-highlight">Arthur (The Butler)</span>: Claims he remained in the pantry polishing the historic sterling silver dining utensils.
            <br>3. <span class="clue-highlight">Dr. Harrison (The Physician)</span>: Claims he fell into a deep sleep in the east wing guest suite after giving Lord Blackwood his evening checkup.
            <br>4. <span class="clue-highlight">Julian (The Estranged Son)</span>: Claims he was in the far library translating an antique scroll regarding the family's land claims.</p>

            <p><strong>THE TWISTS:</strong> Vance mapped the room and spotted inconsistencies that shattered the suspect narratives. Lord Blackwood's evening tea sat perfectly full—untouched. However, the <span class="clue-highlight">antique grandfather clock</span> in the corner, broken for half a century, was mysteriously ticking loud and fast. Most damningly, an open fountain pen lay dropped on the desk next to an unblemished sheet of paper. The air carried a strong smell of bitter almonds—the classic signature of swift cyanide absorption.</p>

            <p>Julian quickly noted that his father’s fingers were entirely clean, lacking any ink marks, suggesting he never wrote anything. Dr. Harrison added that the toxicity was clearly highly concentrated contact poison. Arthur the butler whispered frantically that Lord Blackwood always wrote his personal logs immediately before midnight. Lady Eleanor simply wept, blaming a curse.</p>

            <p>Vance locked the manor doors. The killer believed the locked room cleared them. But the killer missed a vital chronological paradox. The grandfather clock was not ticking due to its gears—it was housing a modern, hidden spring mechanism designed to actuate exactly at midnight, throwing the heavy interior iron door bolts forward via a system of hidden pulleys embedded inside the hollow walls. The room was locked *after* the murder occurred, completely staging the impossibility.</p>
        </div>

        <!-- Interactive Interrogation Form -->
        <div class="interrogation-zone">
            <h2>ACCUSE THE CULPRIT</h2>
            <p>Who used the mechanical system to stage the room and plant the trap?</p>
            
            <select id="suspectCtrl">
                <option value="">-- SELECT SUSPECT --</option>
                <option value="eleanor">Lady Eleanor</option>
                <option value="harrison">Dr. Harrison</option>
                <option value="julian">Julian Blackwood</option>
                <option value="arthur">Arthur the Butler</option>
            </select>
            <br>
            <button class="btn-accuse" onclick="processAccusation()">Submit Final Charge</button>

            <div class="log-output" id="logOutput"></div>
        </div>

        <!-- The Dark Horror Reveal Panel -->
        <div class="horror-reveal" id="horrorReveal">
            <h2 class="horror-title">THE ARCHIVES ARE OPENED</h2>
            <p id="finalStoryText"></p>
            
            <div class="horror-image-container">
                <!-- Built-in High-Contrast Vector Horror Image -->
                <svg viewBox="0 0 200 200" width="100%" height="100%" style="background:#000;">
                    <!-- Distorted background patterns -->
                    <path d="M 0,0 L 200,200 M 200,0 L 0,200" stroke="#110000" stroke-width="4"/>
                    <!-- Ghoulish Abstract Silhouette -->
                    <path d="M60 200 Q40 130 70 90 Q60 60 80 40 Q100 20 120 40 Q140 60 130 90 Q160 130 140 200 Z" fill="#0c0303"/>
                    <!-- Ghostly Face Shadow Structure -->
                    <path d="M75 80 Q100 50 125 80 Q100 120 75 80 Z" fill="#1c0808"/>
                    <!-- Glowing, Empty Demonic Eyes -->
                    <circle cx="90" cy="75" r="5" fill="#ff002c" filter="drop-shadow(0px 0px 5px #ff0000)"/>
                    <circle cx="110" cy="75" r="5" fill="#ff002c" filter="drop-shadow(0px 0px 5px #ff0000)"/>
                    <!-- Distorted, wide jaw line -->
                    <path d="M 85,95 Q 100,115 115,95 Q 100,102 85,95" fill="#000" stroke="#ff002c" stroke-width="1.5"/>
                    <!-- Splatter effects -->
                    <path d="M20 20 L30 40 L25 50 Z M170 40 L160 70 L175 60 Z" fill="#40000a"/>
                    <!-- Static Overlay Bar -->
                    <rect x="0" y="120" width="200" height="8" fill="rgba(255,0,0,0.15)"/>
                </svg>
            </div>
            <p style="color:#666; font-size:0.8rem; text-align:center;">// MALICIOUS ENTITY DETECTED // SYSTEM FAILURE //</p>
        </div>
    </div>

    <script>
        let strikeCount = 0;
        
        // Web Audio Synthesizer Engine Variables
        let audioCtx = null;
        let droneOsc = null;
        let chordOsc = null;
        let filterNode = null;
        let isPlaying = false;

        function toggleAtmosphere() {
            if (isPlaying) {
                stopMusic();
                return;
            }

            try {
                // Initialize Web Audio API context
                audioCtx = new (window.AudioContext || window.webkitAudioContext)();
                
                // Create Low-pass Filter for an ominous, muffled basement atmosphere
                filterNode = audioCtx.createBiquadFilter();
                filterNode.type = 'lowpass';
                filterNode.frequency.setValueAtTime(280, audioCtx.currentTime);

                // 1. Deep Base Drone
                droneOsc = audioCtx.createOscillator();
                droneOsc.type = 'sawtooth';
                droneOsc.frequency.setValueAtTime(55, audioCtx.currentTime); // A1 note
                
                let droneGain = audioCtx.createGain();
                droneGain.gain.setValueAtTime(0.15, audioCtx.currentTime);
                
                droneOsc.connect(droneGain);
                droneGain.connect(filterNode);

                // 2. High Eerie Detuned Chord
                chordOsc = audioCtx.createOscillator();
                chordOsc.type = 'triangle';
                chordOsc.frequency.setValueAtTime(233.08, audioCtx.currentTime); // B-flat minor vibe
                chordOsc.detune.setValueAtTime(15, audioCtx.currentTime);
                
                let chordGain = audioCtx.createGain();
                chordGain.gain.setValueAtTime(0.06, audioCtx.currentTime);
                
                chordOsc.connect(chordGain);
                chordGain.connect(filterNode);

                // Final Output
                filterNode.connect(audioCtx.destination);

                // Start audio generation
                droneOsc.start();
                chordOsc.start();
                
                // Slowly modulate the filter to make it sound like breathing/creeping shadows
                setInterval(() => {
                    if(audioCtx && filterNode) {
                        let wave = 250 + Math.sin(audioCtx.currentTime * 0.5) * 60;
                        filterNode.frequency.setValueAtTime(wave, audioCtx.currentTime);
                    }
                }, 100);

                document.getElementById('audioBtn').innerText = "Deactivate Audio Engine";
                document.getElementById('audioBtn').style.borderColor = "var(--terminal-green)";
                document.getElementById('audioBtn').style.color = "var(--terminal-green)";
                isPlaying = true;

            } catch(e) {
                console.error("Audio engine failed init:", e);
            }
        }

        function stopMusic() {
            if (droneOsc) { droneOsc.stop(); droneOsc.disconnect(); }
            if (chordOsc) { chordOsc.stop(); chordOsc.disconnect(); }
            document.getElementById('audioBtn').innerText = "Initiate Eerie Audio Engine";
            document.getElementById('audioBtn').style.borderColor = "var(--neon-red)";
            document.getElementById('audioBtn').style.color = "var(--neon-red)";
            isPlaying = false;
        }

        function processAccusation() {
            const selectVal = document.getElementById('suspectCtrl').value;
            const output = document.getElementById('logOutput');
            const revealContainer = document.getElementById('horrorReveal');
            const finalStoryText = document.getElementById('finalStoryText');

            if (!selectVal) {
                output.innerHTML = "<span style='color:orange;'>[ERROR: SELECT A SUSPECT COMPONENT]</span>";
                return;
            }

            // Correct Answer is Dr. Harrison (The Doctor who used his medical checkup window to prime the traps)
            if (selectVal === "harrison") {
                output.innerHTML = "<span style='color:var(--terminal-green);'>[CASE SOLVED: ARCHIVE UNLOCKED]</span>";
                finalStoryText.innerHTML = "<strong>CRIMSON CASE STATUS: RESOLVED</strong><br><br>Dr. Harrison was the mastermind. During the evening health checkup, he painted the transparent, deadly cyanide base directly onto the grip of Lord Blackwood's favorite fountain pen. Harrison knew the Lord's absolute habit was to write in his private logs right at midnight. Harrison used his knowledge of the Manor's architectural layout to rig the old grandfather clock weights to the door bolts earlier that afternoon. When the clock struck twelve, the weight dropped, the cables pulled the heavy iron bars into place from the inside, creating a 'perfect' locked-room illusion while Harrison sat safely away in the east wing.";
                revealContainer.style.display = "block";
                revealContainer.scrollIntoView({ behavior: 'smooth' });
            } else {
                strikeCount++;
                if (strikeCount === 1) {
                    output.innerHTML = "<span style='color:var(--neon-red);'>[WARNING: ALIBI VERIFIED. TARGET INNOCENT. TRY AGAIN]</span>";
                } else {
                    output.innerHTML = "<span style='color:#ff0000; font-size:1.2rem;'>[SYSTEM CRITICAL FAILURE: ENTITY BREACH]</span>";
                    
                    // Force the horrific breakdown reveal
                    finalStoryText.innerHTML = "<strong>CASE STATUS: COMPROMISED</strong><br><br>Your deduction failed. The delay allowed the actual killer, <strong>Dr. Harrison</strong>, to clear his tracks and escape into the winter storm. He poisoned the fountain pen's grip during the checkup and rigged the grandfather clock to drop the door bolts exactly at midnight via dynamic internal pulley frames. Because you targeted an innocent soul, the dark curse of Crimson Manor has manifested to consume the investigation files entirely...";
                    
                    revealContainer.style.display = "block";
                    
                    // Flash screen red for extreme horror impact
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
