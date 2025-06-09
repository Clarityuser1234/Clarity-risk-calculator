
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Appendicitis Risk Stratification</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Inter', sans-serif;
            background-color: #ffffff; /* White background */
        }
        .container {
            max-width: 960px;
            margin: 2rem auto;
            padding: 2.5rem;
            background-color: #ffffff;
            border-radius: 12px;
            box-shadow: 0 6px 20px rgba(0, 0, 0, 0.1);
            display: flex;
            flex-direction: column;
            gap: 2rem;
        }
        .section-title {
            font-size: 2.25rem;
            font-weight: 700;
            color: #000000; /* Black */
            text-align: center;
            margin-bottom: 1.5rem;
        }
        .sub-section-title {
            font-size: 1.75rem;
            font-weight: 600;
            color: #000000; /* Black */
            margin-bottom: 1.25rem;
        }
        .input-group {
            margin-bottom: 1.5rem;
        }
        .label {
            display: block;
            font-weight: 600;
            margin-bottom: 0.5rem;
            color: #000000; /* Black */
        }
        .btn {
            padding: 0.75rem 1.75rem;
            border-radius: 8px;
            font-weight: 600;
            cursor: pointer;
            transition: background-color 0.2s ease, transform 0.1s ease;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.06);
        }
        .btn:active {
            transform: translateY(1px);
        }
        .btn-primary {
            background-color: #f97316; /* Orange 500 */
            color: #ffffff;
        }
        .btn-primary:hover {
            background-color: #ea580c; /* Orange 600 */
        }
        .btn-secondary {
            background-color: #ffffff; /* White */
            color: #000000; /* Black */
            border: 1px solid #000000; /* Black border */
        }
        .btn-secondary:hover {
            background-color: #e5e7eb; /* Light gray for hover */
        }
        .score-display {
            background-color: #fff7ed; /* Orange 50 */
            border-left: 4px solid #f97316; /* Orange 500 border */
            padding: 1.5rem;
            border-radius: 8px;
            margin-top: 2rem;
            color: #000000; /* Black text */
        }
        .score-display h3 {
            font-weight: 700;
            margin-bottom: 0.75rem;
            color: #c2410c; /* Orange 800 */
        }
        /* Style for the range input (slider) */
        input[type="range"] {
            -webkit-appearance: none;
            width: 100%;
            height: 8px;
            background: #d1d5db;
            outline: none;
            border-radius: 5px;
            opacity: 0.7;
            transition: opacity .2s;
        }

        input[type="range"]:hover {
            opacity: 1;
        }

        input[type="range"]::-webkit-slider-thumb {
            -webkit-appearance: none;
            appearance: none;
            width: 20px;
            height: 20px;
            background: #f97316; /* Orange 500 */
            cursor: pointer;
            border-radius: 50%;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
        }

        input[type="range"]::-moz-range-thumb {
            width: 20px;
            height: 20px;
            background: #f97316; /* Orange 500 */
            cursor: pointer;
            border-radius: 50%;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
        }
        select, input[type="radio"] {
            border-color: #d1d5db;
        }
        input[type="radio"]:checked {
            background-color: #f97316; /* Orange 500 */
            border-color: #f97316; /* Orange 500 */
        }
        .checkbox-item {
            display: flex;
            align-items: center;
            margin-bottom: 0.75rem;
        }
        .checkbox-item input[type="checkbox"] {
            margin-right: 0.75rem;
            height: 1.25rem;
            width: 1.25rem;
            border-radius: 4px;
            border-color: #000000; /* Black border */
            color: #f97316; /* Orange checkmark */
        }
        .checkbox-item label {
            font-weight: 500;
            color: #000000; /* Black */
        }
        /* Style for cells in the checklist grid for consistent padding */
        .checklist-grid > div {
            padding-top: 0.75rem;
            padding-bottom: 0.75rem;
        }
    </style>
</head>
<body class="bg-white min-h-screen flex items-center justify-center">
    <div class="container">
        <h1 class="section-title">Appendicitis risk stratification</h1>

        <!-- Disclaimer -->
        <div class="bg-amber-100 border-l-4 border-amber-500 text-amber-700 p-4 rounded-md mb-6" role="alert">
            <p class="font-bold">Disclaimer:</p>
            <p class="text-sm">This tool is for informational and educational purposes only, based on the provided document. It is not intended to be a substitute for professional medical advice, diagnosis, or treatment. Always seek the advice of your physician or other qualified health provider with any questions you may have regarding a medical condition.</p>
        </div>

        <!-- Gender Selection -->
        <div id="gender-selection" class="input-group">
            <label class="label text-xl mb-4">Please select patient's gender:</label>
            <div class="flex flex-col sm:flex-row space-y-3 sm:space-y-0 sm:space-x-8">
                <label class="inline-flex items-center">
                    <input type="radio" name="gender" value="female" class="form-radio h-6 w-6 text-orange-600 rounded-full border-gray-300 focus:ring-orange-500">
                    <span class="ml-3 text-lg text-black font-medium">Female</span>
                </label>
                <label class="inline-flex items-center">
                    <input type="radio" name="gender" value="male" class="form-radio h-6 w-6 text-orange-600 rounded-full border-gray-300 focus:ring-orange-500">
                    <span class="ml-3 text-lg text-black font-medium">Male</span>
                </label>
            </div>
        </div>

        <!-- AAS Questionnaire (Female) -->
        <div id="aas-form" class="hidden p-6 bg-orange-50 rounded-lg shadow-sm border border-orange-200">
            <h2 class="sub-section-title text-center text-orange-700">Female: Adult Appendicitis Score (AAS)</h2>
            <p class="text-sm text-black mb-6 text-center">Please answer the following questions to calculate the AAS score.</p>

            <!-- Age Input - Slider -->
            <div class="input-group">
                <label for="aas-age" class="label">Age: <span id="aas-age-value" class="font-bold text-orange-700">16</span></label>
                <input type="range" id="aas-age" min="16" max="39" value="16" class="mt-1 block w-full">
            </div>

            <div class="input-group">
                <label class="label">RLQ Pain?</label>
                <div class="flex flex-col sm:flex-row space-y-2 sm:space-y-0 sm:space-x-4">
                    <label class="inline-flex items-center">
                        <input type="radio" name="aas-rlq-pain" value="2" class="form-radio h-4 w-4 text-orange-600 rounded-full border-gray-300">
                        <span class="ml-2 text-black">Yes (+2)</span>
                    </label>
                    <label class="inline-flex items-center">
                        <input type="radio" name="aas-rlq-pain" value="0" class="form-radio h-4 w-4 text-orange-600 rounded-full border-gray-300">
                        <span class="ml-2 text-black">No (0)</span>
                    </label>
                </div>
            </div>

            <div class="input-group">
                <label class="label">Pain Relocation/ Migratory Pain?</label>
                <div class="flex flex-col sm:flex-row space-y-2 sm:space-y-0 sm:space-x-4">
                    <label class="inline-flex items-center">
                        <input type="radio" name="aas-pain-relocation" value="2" class="form-radio h-4 w-4 text-orange-600 rounded-full border-gray-300">
                        <span class="ml-2 text-black">Yes (+2)</span>
                    </label>
                    <label class="inline-flex items-center">
                        <input type="radio" name="aas-pain-relocation" value="0" class="form-radio h-4 w-4 text-orange-600 rounded-full border-gray-300">
                        <span class="ml-2 text-black">No (0)</span>
                    </label>
                </div>
            </div>
            
            <!-- RLQ Tenderness question (reordered) -->
            <div class="input-group">
                <label class="label">RLQ Tenderness:</label>
                <div class="flex flex-col sm:flex-row space-y-2 sm:space-y-0 sm:space-x-4">
                    <label class="inline-flex items-center">
                        <input type="radio" name="aas-rlq-tenderness" value="1" class="form-radio h-4 w-4 text-orange-600 rounded-full border-gray-300">
                        <span class="ml-2 text-black">Yes (+1)</span>
                    </label>
                    <label class="inline-flex items-center">
                        <input type="radio" name="aas-rlq-tenderness" value="0" class="form-radio h-4 w-4 text-orange-600 rounded-full border-gray-300">
                        <span class="ml-2 text-black">No (0)</span>
                    </label>
                </div>
            </div>

            <!-- Guarding question (reordered) -->
            <div class="input-group">
                <label class="label">Guarding?:</label>
                <div class="flex flex-col space-y-2">
                    <label class="inline-flex items-center">
                        <input type="radio" name="aas-guarding" value="0" class="form-radio h-4 w-4 text-orange-600 rounded-full border-gray-300">
                        <span class="ml-2 text-black">None (0)</span>
                    </label>
                    <label class="inline-flex items-center">
                        <input type="radio" name="aas-guarding" value="2" class="form-radio h-4 w-4 text-orange-600 rounded-full border-gray-300">
                        <span class="ml-2 text-black">Mild (+2)</span>
                    </label>
                    <label class="inline-flex items-center">
                        <input type="radio" name="aas-guarding" value="4" class="form-radio h-4 w-4 text-orange-600 rounded-full border-gray-300">
                        <span class="ml-2 text-black">Mod Or Severe (+4)</span>
                    </label>
                </div>
            </div>
            <!-- End Reordered -->

            <!-- Changed to slider for WCC -->
            <div class="input-group">
                <label for="aas-wcc" class="label">Total WCC: <span id="aas-wcc-value" class="font-bold text-orange-700">1.0</span></label>
                <input type="range" id="aas-wcc" min="1" max="40" value="1.0" step="0.1" class="mt-1 block w-full">
            </div>

            <!-- Changed to slider for Neutrophils % -->
            <div class="input-group">
                <label for="aas-neutrophils-count" class="label">Neutrophils (Count): <span id="aas-neutrophils-count-value" class="font-bold text-orange-700">1.0</span></label>
                <input type="range" id="aas-neutrophils-count" min="1" max="40" value="1.0" step="0.1" class="mt-1 block w-full">
                <p class="text-sm text-black mt-1">Enter raw count for neutrophils; percentage will be calculated against Total WCC.</p>
            </div>

            <div class="input-group">
                <label class="label">Symptom Duration for CRP:</label>
                <div class="flex flex-col sm:flex-row space-y-2 sm:space-y-0 sm:space-x-4">
                    <label class="inline-flex items-center">
                        <input type="radio" name="aas-symptom-duration" value="less-24" class="form-radio h-4 w-4 text-orange-600 rounded-full border-gray-300">
                        <span class="ml-2 text-black">Less than 24 Hours</span>
                    </label>
                    <label class="inline-flex items-center">
                        <input type="radio" name="aas-symptom-duration" value="greater-24" class="form-radio h-4 w-4 text-orange-600 rounded-full border-gray-300">
                        <span class="ml-2 text-black">Greater than or equal to 24 Hours</span>
                    </label>
                </div>
            </div>

            <div class="input-group" id="aas-crp-less-24" style="display:none;">
                <label class="label">CRP (mg/L), Symptoms <24Hrs:</label>
                <div class="flex flex-col space-y-2">
                    <label class="inline-flex items-center">
                        <input type="radio" name="aas-crp" value="0" class="form-radio h-4 w-4 text-orange-600 rounded-full border-gray-300">
                        <span class="ml-2 text-black">Less than 4 (0)</span>
                    </label>
                    <label class="inline-flex items-center">
                        <input type="radio" name="aas-crp" value="2" class="form-radio h-4 w-4 text-orange-600 rounded-full border-gray-300">
                        <span class="ml-2 text-black">4 – 11 (+2)</span>
                    </label>
                    <label class="inline-flex items-center">
                        <input type="radio" name="aas-crp" value="3" class="form-radio h-4 w-4 text-orange-600 rounded-full border-gray-300">
                        <span class="ml-2 text-black">11 – 25 (+3)</span>
                    </label>
                    <label class="inline-flex items-center">
                        <input type="radio" name="aas-crp" value="5" class="form-radio h-4 w-4 text-orange-600 rounded-full border-gray-300">
                        <span class="ml-2 text-black">25 – 83 (+5)</span>
                    </label>
                    <label class="inline-flex items-center">
                        <input type="radio" name="aas-crp" value="1" class="form-radio h-4 w-4 text-orange-600 rounded-full border-gray-300">
                        <span class="ml-2 text-black">Greater than or equal to 83 (+1)</span>
                    </label>
                </div>
            </div>

            <div class="input-group" id="aas-crp-greater-24" style="display:none;">
                <label class="label">CRP (mg/L), Symptoms more than 24 hours:</label>
                <div class="flex flex-col space-y-2">
                    <label class="inline-flex items-center">
                        <input type="radio" name="aas-crp" value="0" class="form-radio h-4 w-4 text-orange-600 rounded-full border-gray-300">
                        <span class="ml-2 text-black">Less than 12 (0)</span>
                    </label>
                    <label class="inline-flex items-center">
                        <input type="radio" name="aas-crp" value="2" class="form-radio h-4 w-4 text-orange-600 rounded-full border-gray-300">
                        <span class="ml-2 text-black">12 – 53 (+2)</span>
                    </label>
                    <label class="inline-flex items-center">
                        <input type="radio" name="aas-crp" value="2" class="form-radio h-4 w-4 text-orange-600 rounded-full border-gray-300">
                        <span class="ml-2 text-black">53 – 152 (+2)</span>
                    </label>
                    <label class="inline-flex items-center">
                        <input type="radio" name="aas-crp" value="1" class="form-radio h-4 w-4 text-orange-600 rounded-full border-gray-300">
                        <span class="ml-2 text-black">Greater than or equal to 152 (+1)</span>
                    </label>
                </div>
            </div>

            <div class="flex justify-center space-x-4 mt-6">
                <button id="calculate-aas" class="btn btn-primary">Calculate AAS Score</button>
                <button id="reset-aas" class="btn btn-secondary">Reset AAS Form</button>
            </div>
        </div>

        <!-- AIRS Questionnaire (Male) -->
        <div id="airs-form" class="hidden p-6 bg-orange-50 rounded-lg shadow-sm border border-orange-200">
            <h2 class="sub-section-title text-center text-orange-700">Male: Appendicitis Inflammatory Response Score (AIRS)</h2>
            <p class="text-sm text-black mb-6 text-center">Please answer the following questions to calculate the AIRS score.</p>

            <!-- Age Input - Slider -->
            <div class="input-group">
                <label for="airs-age" class="label">Age: <span id="airs-age-value" class="font-bold text-orange-700">16</span></label>
                <input type="range" id="airs-age" min="16" max="39" value="16" class="mt-1 block w-full">
            </div>

            <div class="input-group">
                <label class="label">Vomiting?</label>
                <div class="flex flex-col sm:flex-row space-y-2 sm:space-y-0 sm:space-x-4">
                    <label class="inline-flex items-center">
                        <input type="radio" name="airs-vomiting" value="1" class="form-radio h-4 w-4 text-orange-600 rounded-full border-gray-300">
                        <span class="ml-2 text-black">Yes (+1)</span>
                    </label>
                    <label class="inline-flex items-center">
                        <input type="radio" name="airs-vomiting" value="0" class="form-radio h-4 w-4 text-orange-600 rounded-full border-gray-300">
                        <span class="ml-2 text-black">No (0)</span>
                    </label>
                </div>
            </div>

            <div class="input-group">
                <label class="label">RIF Pain?</label>
                <div class="flex flex-col sm:flex-row space-y-2 sm:space-y-0 sm:space-x-4">
                    <label class="inline-flex items-center">
                        <input type="radio" name="airs-rif-pain" value="1" class="form-radio h-4 w-4 text-orange-600 rounded-full border-gray-300">
                        <span class="ml-2 text-black">Yes (+1)</span>
                    </label>
                    <label class="inline-flex items-center">
                        <input type="radio" name="airs-rif-pain" value="0" class="form-radio h-4 w-4 text-orange-600 rounded-full border-gray-300">
                        <span class="ml-2 text-black">No (0)</span>
                    </label>
                </div>
            </div>

            <div class="input-group">
                <label class="label">Rebound Tenderness:</label>
                <div class="flex flex-col space-y-2">
                    <label class="inline-flex items-center">
                        <input type="radio" name="airs-rebound-tenderness" value="0" class="form-radio h-4 w-4 text-orange-600 rounded-full border-gray-300">
                        <span class="ml-2 text-black">None (0)</span>
                    </label>
                    <label class="inline-flex items-center">
                        <input type="radio" name="airs-rebound-tenderness" value="1" class="form-radio h-4 w-4 text-orange-600 rounded-full border-gray-300">
                        <span class="ml-2 text-black">Light (+1)</span>
                    </label>
                    <label class="inline-flex items-center">
                        <input type="radio" name="airs-rebound-tenderness" value="2" class="form-radio h-4 w-4 text-orange-600 rounded-full border-gray-300">
                        <span class="ml-2 text-black">Medium (+2)</span>
                    </label>
                    <label class="inline-flex items-center">
                        <input type="radio" name="airs-rebound-tenderness" value="3" class="form-radio h-4 w-4 text-orange-600 rounded-full border-gray-300">
                        <span class="ml-2 text-black">Strong (+3)</span>
                    </label>
                </div>
            </div>

            <div class="input-group">
                <label class="label">Temperature greater than 38.5 degrees?</label>
                <div class="flex flex-col sm:flex-row space-y-2 sm:space-y-0 sm:space-x-4">
                    <label class="inline-flex items-center">
                        <input type="radio" name="airs-temp" value="1" class="form-radio h-4 w-4 text-orange-600 rounded-full border-gray-300">
                        <span class="ml-2 text-black">Yes (+1)</span>
                    </label>
                    <label class="inline-flex items-center">
                        <input type="radio" name="airs-temp" value="0" class="form-radio h-4 w-4 text-orange-600 rounded-full border-gray-300">
                        <span class="ml-2 text-black">No (0)</span>
                    </label>
                </div>
            </div>

            <!-- Changed to slider for WCC -->
            <div class="input-group">
                <label for="airs-wcc" class="label">Total WCC: <span id="airs-wcc-value" class="font-bold text-orange-700">1.0</span></label>
                <input type="range" id="airs-wcc" min="1" max="40" value="1.0" step="0.1" class="mt-1 block w-full">
            </div>

            <!-- Changed to slider for Neutrophils % -->
            <div class="input-group">
                <label for="airs-neutrophils-count" class="label">Neutrophils (Count): <span id="airs-neutrophils-count-value" class="font-bold text-orange-700">1.0</span></label>
                <input type="range" id="airs-neutrophils-count" min="1" max="40" value="1.0" step="0.1" class="mt-1 block w-full">
                <p class="text-sm text-black mt-1">Enter raw count for neutrophils; percentage will be calculated against Total WCC.</p>
            </div>

            <div class="input-group">
                <label class="label">CRP, mg/L:</label>
                <div class="flex flex-col space-y-2">
                    <label class="inline-flex items-center">
                        <input type="radio" name="airs-crp" value="0" class="form-radio h-4 w-4 text-orange-600 rounded-full border-gray-300">
                        <span class="ml-2 text-black">Less than 10 (0)</span>
                    </label>
                    <label class="inline-flex items-center">
                        <input type="radio" name="airs-crp" value="1" class="form-radio h-4 w-4 text-orange-600 rounded-full border-gray-300">
                        <span class="ml-2 text-black">10 – 49 (+1)</span>
                    </label>
                    <label class="inline-flex items-center">
                        <input type="radio" name="airs-crp" value="2" class="form-radio h-4 w-4 text-orange-600 rounded-full border-gray-300">
                        <span class="ml-2 text-black">Greater than or equal to 50 (+2)</span>
                    </label>
                </div>
            </div>

            <div class="flex justify-center space-x-4 mt-6">
                <button id="calculate-airs" class="btn btn-primary">Calculate AIRS Score</button>
                <button id="reset-airs" class="btn btn-secondary">Reset AIRS Form</button>
            </div>
        </div>

        <!-- Results Display -->
        <div id="results-display" class="score-display">
            <h3 class="text-xl font-bold mb-2">Your Risk Score: <span id="score-value"></span></h3>
            <p id="score-interpretation" class="text-black"></p>
            <button id="reset-all" class="btn btn-secondary mt-4">Start Over</button>
        </div>

        <!-- Checklist Section -->
        <div id="clarity-checklist" class="p-6 bg-white rounded-lg shadow-sm border border-gray-800">
            <h2 class="sub-section-title text-center text-orange-700">Clarity Checklist</h2>
            <p class="text-black mb-6 text-center">Track completion of key assessment steps.</p>

            <div class="grid checklist-grid grid-cols-[1.5fr_1.2fr_1.2fr_1.2fr_auto] gap-x-6 gap-y-3 items-stretch text-sm">
                <!-- Header Row -->
                <div class="font-bold text-black text-base border-b border-black pb-2">Step</div>
                <div class="font-bold text-black text-base border-b border-black pb-2 text-center">Low Risk</div>
                <div class="font-bold text-black text-base border-b border-black pb-2 text-center">Medium Risk</div>
                <div class="font-bold text-black text-base border-b border-black pb-2 text-center">High Risk</div>
                <div class="font-bold text-black text-base border-b border-black pb-2 text-right">Completed</div>

                <!-- Step 1 - Entire Row -->
                <div class="py-2 flex flex-col justify-between">
                    <div>
                        <h3 class="font-semibold text-black mb-1">STEP 1: Risk Stratification</h3>
                        <p class="text-xs text-black">a) What is the calculated risk score?</p>
                    </div>
                    <div class="border-b border-black w-full my-4"></div> <!-- Line only in this column, tripled space -->
                    <div>
                        <p class="text-xs text-black">b) Based on clinical assessment of medium-high risk patients, is appendicitis likely?</p>
                    </div>
                </div>

                <!-- Column 2: Low Risk (Step 1) -->
                <div class="py-2 flex flex-col justify-between text-center">
                    <div>
                        <p class="text-xs text-black">Female: AAS &le; 8</p>
                        <p class="text-xs text-black">Male: AIRS &le; 2</p>
                    </div>
                    <!-- Spacer to push content down for alignment -->
                    <div class="flex-grow"></div>
                    <div>
                        <p class="text-xs text-black"></p> <!-- Blank for b) -->
                    </div>
                </div>

                <!-- Column 3: Medium Risk (Step 1) -->
                <div class="py-2 flex flex-col justify-between text-center">
                    <div>
                        <p class="text-xs text-black">Female: AAS &ge; 9</p>
                        <p class="text-xs text-black">Male: AIRS &ge; 3</p>
                    </div>
                    <!-- Spacer to push content down for alignment -->
                    <div class="flex-grow"></div>
                    <div>
                        <p class="text-xs text-black">Indeterminate</p>
                    </div>
                </div>

                <!-- Column 4: High Risk (Step 1) -->
                <div class="py-2 flex flex-col justify-between text-center">
                    <div>
                        <p class="text-xs text-black">Female: AAS &ge; 9</p>
                        <p class="text-xs text-black">Male: AIRS &ge; 3</p>
                    </div>
                    <!-- Spacer to push content down for alignment -->
                    <div class="flex-grow"></div>
                    <div>
                        <p class="text-xs text-black">Likely Appendicitis</p>
                    </div>
                </div>

                <!-- Column 5: Completed Checkbox (Step 1) -->
                <div class="py-2 self-center text-right">
                    <input type="checkbox" id="step1-completed" class="form-checkbox h-5 w-5 text-orange-600 rounded">
                </div>
                <!-- End Step 1 -->

                <!-- Step 2 -->
                <div class="border-t border-black pt-3 py-2">
                    <h3 class="font-semibold text-black mb-1">STEP 2: Care Pathway</h3>
                    <p class="text-xs text-black">Is the patient on an appropriate care pathway?</p>
                </div>
                <div class="text-center border-t border-black pt-3 py-2 flex items-center justify-center">
                    <div>
                        <p class="text-xs text-black">Home</p>
                        <p class="text-[0.65rem] text-black mt-1">(For symptom onset &lt;24hours: consider ambulatory follow up)</p>
                    </div>
                </div>
                <div class="text-center border-t border-black pt-3 py-2 flex items-center justify-center">
                    <p class="text-xs text-black">Ambulatory Review in 24hrs</p>
                </div>
                <div class="text-center border-t border-black pt-3 py-2 flex items-center justify-center">
                    <p class="text-xs text-black">Admit</p>
                </div>
                <div class="border-t border-black pt-3 py-2 flex items-center justify-end pr-2"> <!-- Added flex and pr-2 for consistent alignment -->
                    <input type="checkbox" id="step2-completed" class="form-checkbox h-5 w-5 text-orange-600 rounded">
                </div>
                
                <!-- Step 3 -->
                <div class="border-t border-black pt-3 py-2">
                    <h3 class="font-semibold text-black mb-1">STEP 3: Selective Imaging</h3>
                </div>
                <div class="text-center border-t border-black pt-3 py-2 flex items-center justify-center">
                    <p class="text-[0.65rem] text-black italic">(For cases of clinical concern or upon re-attendance: refer to medium risk column)</p>
                </div>
                <div class="text-center border-t border-black pt-3 py-2 flex items-center justify-center">
                    <div>
                        <p class="text-xs text-black">Consider LDCT if symptoms persist</p>
                        <p class="text-xs text-black mt-1">Refer if alternate diagnosis suspected</p>
                    </div>
                </div>
                <div class="text-center border-t border-black pt-3 py-2 flex items-center justify-center">
                    <p class="text-xs text-black">Consider LDCT before surgery</p>
                </div>
                <div class="border-t border-black pt-3 py-2 flex items-center justify-end pr-2"> <!-- Added flex and pr-2 for consistent alignment -->
                    <input type="checkbox" id="step3-completed" class="form-checkbox h-5 w-5 text-orange-600 rounded">
                </div>

                <!-- Step 4 -->
                <div class="border-t border-black pt-3 py-2">
                    <h3 class="font-semibold text-black mb-1">STEP 4: Management</h3>
                    <p class="text-xs text-black">Did Low dose CT show evidence of appendicitis?</p>
                </div>
                <div class="text-center border-t border-black pt-3 py-2">
                </div>
                <div class="text-center border-t border-black pt-3 py-2 flex items-center justify-center">
                    <div>
                        <p class="text-xs text-black">Yes - Treat Appendicitis</p>
                        <p class="text-xs text-black mt-1">No - Home</p>
                    </div>
                </div>
                <div class="text-center border-t border-black pt-3 py-2 flex items-center justify-center">
                    <div>
                        <p class="text-xs text-black">Yes - Treat Appendicitis</p>
                        <p class="text-xs text-black mt-1">No - Home</p>
                        <p class="text-[0.65rem] text-black mt-1 italic">(For ongoing clinical concern: consider monitoring or referral)</p>
                    </div>
                </div>
                <div class="border-t border-black pt-3 py-2 flex items-center justify-end pr-2"> <!-- Added flex and pr-2 for consistent alignment -->
                    <input type="checkbox" id="step4-completed" class="form-checkbox h-5 w-5 text-orange-600 rounded">
                </div>
            </div>
            <div class="text-center mt-6">
                <button id="reset-checklist" class="btn btn-secondary">Reset Checklist</button>
            </div>
        </div>

        <div class="text-center mt-6">
            <button id="copy-answers" class="btn btn-primary">Copy Answers Summary</button>
        </div>
    </div>

    <script>
        // Get references to HTML elements
        const genderSelection = document.getElementById('gender-selection');
        const aasForm = document.getElementById('aas-form');
        const airsForm = document.getElementById('airs-form');
        const resultsDisplay = document.getElementById('results-display');
        const scoreValueSpan = document.getElementById('score-value');
        const scoreInterpretationParagraph = document.getElementById('score-interpretation');

        const aasAgeSelect = document.getElementById('aas-age');
        const aasAgeValueSpan = document.getElementById('aas-age-value');
        const airsAgeSelect = document.getElementById('airs-age');
        const airsAgeValueSpan = document.getElementById('airs-age-value');

        // Elements for AIRS WCC and Neutrophils sliders
        const airsWccSlider = document.getElementById('airs-wcc');
        const airsWccValueSpan = document.getElementById('airs-wcc-value');
        const airsNeutrophilsCountSlider = document.getElementById('airs-neutrophils-count');
        const airsNeutrophilsCountValueSpan = document.getElementById('airs-neutrophils-count-value');

        // New elements for AAS WCC and Neutrophils sliders
        const aasWccSlider = document.getElementById('aas-wcc');
        const aasWccValueSpan = document.getElementById('aas-wcc-value');
        const aasNeutrophilsCountSlider = document.getElementById('aas-neutrophils-count');
        const aasNeutrophilsCountValueSpan = document.getElementById('aas-neutrophils-count-value');


        const aasCrpLess24 = document.getElementById('aas-crp-less-24');
        const aasCrpGreater24 = document.getElementById('aas-crp-greater-24');

        const calculateAasBtn = document.getElementById('calculate-aas');
        const resetAasBtn = document.getElementById('reset-aas');
        const calculateAirsBtn = document.getElementById('calculate-airs');
        const resetAirsBtn = document.getElementById('reset-airs');
        const resetAllBtn = document.getElementById('reset-all');
        const copyAnswersBtn = document.getElementById('copy-answers');

        // Initialize age display values
        aasAgeValueSpan.textContent = aasAgeSelect.value;
        airsAgeValueSpan.textContent = airsAgeSelect.value;

        // Initialize WCC and Neutrophils display values for AIRS
        airsWccValueSpan.textContent = parseFloat(airsWccSlider.value).toFixed(1);
        airsNeutrophilsCountValueSpan.textContent = parseFloat(airsNeutrophilsCountSlider.value).toFixed(1);

        // Initialize WCC and Neutrophils display values for AAS
        aasWccValueSpan.textContent = parseFloat(aasWccSlider.value).toFixed(1);
        aasNeutrophilsCountValueSpan.textContent = parseFloat(aasNeutrophilsCountSlider.min).toFixed(1); // Set to min on load
        aasNeutrophilsCountSlider.value = parseFloat(aasNeutrophilsCountSlider.min);


        // Add event listeners for age sliders
        aasAgeSelect.addEventListener('input', (event) => {
            aasAgeValueSpan.textContent = event.target.value;
            calculateAASScore(); // Recalculate on age change
        });

        airsAgeSelect.addEventListener('input', (event) => {
            airsAgeValueSpan.textContent = event.target.value;
            calculateAIRSScore(); // Recalculate on age change
        });

        // Add event listeners for new AIRS sliders (WCC and Neutrophils)
        airsWccSlider.addEventListener('input', (event) => {
            airsWccValueSpan.textContent = parseFloat(event.target.value).toFixed(1);
            calculateAIRSScore(); // Recalculate on WCC change
        });

        airsNeutrophilsCountSlider.addEventListener('input', (event) => {
            airsNeutrophilsCountValueSpan.textContent = parseFloat(event.target.value).toFixed(1);
            calculateAIRSScore(); // Recalculate on Neutrophils change
        });

        // Add event listeners for new AAS sliders (WCC and Neutrophils)
        aasWccSlider.addEventListener('input', (event) => {
            aasWccValueSpan.textContent = parseFloat(event.target.value).toFixed(1);
            calculateAASScore(); // Recalculate on WCC change
        });

        aasNeutrophilsCountSlider.addEventListener('input', (event) => {
            aasNeutrophilsCountValueSpan.textContent = parseFloat(event.target.value).toFixed(1);
            calculateAASScore(); // Recalculate on Neutrophils change
        });


        // Function to get selected radio button value
        function getRadioValue(name) {
            const radios = document.getElementsByName(name);
            for (const radio of radios) {
                if (radio.checked) {
                    return parseFloat(radio.value); // Use parseFloat as values are now ints or can be converted to floats
                }
            }
            return null; // Return null if no option is selected
        }

        // Function to reset a specific form
        function resetForm(formId) {
            const form = document.getElementById(formId);
            const radioButtons = form.querySelectorAll('input[type="radio"]');
            radioButtons.forEach(radio => radio.checked = false);

            // Reset sliders to min value and update display
            if (formId === 'aas-form') {
                aasAgeSelect.value = aasAgeSelect.min;
                aasAgeValueSpan.textContent = aasAgeSelect.min;
                // Reset AAS sliders
                aasWccSlider.value = parseFloat(aasWccSlider.min).toFixed(1);
                aasWccValueSpan.textContent = parseFloat(aasWccSlider.min).toFixed(1);
                aasNeutrophilsCountSlider.value = parseFloat(aasNeutrophilsCountSlider.min).toFixed(1);
                aasNeutrophilsCountValueSpan.textContent = parseFloat(aasNeutrophilsCountSlider.min).toFixed(1);
            } else if (formId === 'airs-form') {
                airsAgeSelect.value = airsAgeSelect.min;
                airsAgeValueSpan.textContent = airsAgeSelect.min;
                // Also reset new AIRS sliders
                airsWccSlider.value = parseFloat(airsWccSlider.min).toFixed(1);
                airsWccValueSpan.textContent = parseFloat(airsWccSlider.min).toFixed(1);
                airsNeutrophilsCountSlider.value = parseFloat(airsNeutrophilsCountSlider.min).toFixed(1);
                airsNeutrophilsCountValueSpan.textContent = parseFloat(airsNeutrophilsCountSlider.min).toFixed(1);
            }

            scoreValueSpan.textContent = ''; // Clear score display
            scoreInterpretationParagraph.textContent = ''; // Clear interpretation
            resultsDisplay.classList.add('hidden'); // Hide results when form is reset (will be shown on gender selection)

            // Hide CRP sections for AAS form
            if (formId === 'aas-form') {
                aasCrpLess24.style.display = 'none';
                aasCrpGreater24.style.display = 'none';
                // Also uncheck the symptom duration radios
                document.querySelectorAll('input[name="aas-symptom-duration"]').forEach(radio => radio.checked = false);
            }
        }

        // Function to reset the checklist
        function resetChecklist() {
            document.querySelectorAll('#clarity-checklist input[type="checkbox"]').forEach(checkbox => {
                checkbox.checked = false;
            });
        }

        // --- Core Calculation Functions ---

        function calculateAASScore() {
            let score = 0;
            const age = parseInt(aasAgeSelect.value, 10);

            // Check if age is selected (always is with slider now, but can be NaN if initial value is not number)
            if (isNaN(age)) {
                scoreValueSpan.textContent = '';
                scoreInterpretationParagraph.textContent = 'Please select patient\'s age.';
                resultsDisplay.classList.remove('hidden'); // Show results display to show message
                return;
            }

            // Get slider values for AAS - Use parseFloat
            const aasWccValue = parseFloat(aasWccSlider.value);
            const aasNeutrophilsCountValue = parseFloat(aasNeutrophilsCountSlider.value);

            // Validate slider values for calculation
            if (isNaN(aasWccValue) || isNaN(aasNeutrophilsCountValue)) {
                scoreValueSpan.textContent = '';
                scoreInterpretationParagraph.textContent = 'Please provide values for Total WCC and Neutrophils Count.';
                resultsDisplay.classList.remove('hidden');
                return;
            }
            if (aasWccValue === 0) { // Prevent division by zero
                scoreValueSpan.textContent = '';
                scoreInterpretationParagraph.textContent = 'Total WCC cannot be zero for neutrophil percentage calculation.';
                resultsDisplay.classList.remove('hidden');
                return;
            }


            // AAS Score calculation logic based on PDF
            // Ensure all required radio buttons for AAS are selected.
            const requiredAasRadioQuestions = [
                'aas-rlq-pain',
                'aas-pain-relocation',
                'aas-guarding',
                'aas-rlq-tenderness',
                'aas-symptom-duration' // Check if duration is selected
            ];
            let allAasRadiosAnswered = true;
            for (const qName of requiredAasRadioQuestions) {
                if (getRadioValue(qName) === null) {
                    allAasRadiosAnswered = false;
                    break;
                }
            }

            // Check CRP specifically, as it's conditional
            const symptomDurationSelected = document.querySelector('input[name="aas-symptom-duration"]:checked');
            let crpAnswered = false;
            if (symptomDurationSelected) {
                const crpRadiosLess24 = document.querySelectorAll('#aas-crp-less-24 input[name="aas-crp"]');
                const crpRadiosGreater24 = document.querySelectorAll('#aas-crp-greater-24 input[name="aas-crp"]');

                if (aasCrpLess24.style.display === 'block') {
                    crpRadiosLess24.forEach(radio => { if (radio.checked) crpAnswered = true; });
                } else if (aasCrpGreater24.style.display === 'block') {
                    crpRadiosGreater24.forEach(radio => { if (radio.checked) crpAnswered = true; });
                }
            }

            if (!allAasRadiosAnswered || !crpAnswered) {
                scoreValueSpan.textContent = '';
                scoreInterpretationParagraph.textContent = 'Please answer all questions to calculate the score.';
                resultsDisplay.classList.remove('hidden');
                return;
            }

            // Proceed with calculation if all inputs are available
            score += getRadioValue('aas-rlq-pain');
            score += getRadioValue('aas-pain-relocation');
            score += getRadioValue('aas-guarding');
            score += getRadioValue('aas-rlq-tenderness');
            
            // WCC scoring for AAS
            if (aasWccValue < 7.2) {
                // Score remains 0
            } else if (aasWccValue >= 7.2 && aasWccValue < 10.9) {
                score += 1;
            } else if (aasWccValue >= 10.9 && aasWccValue < 14) {
                score += 2;
            } else if (aasWccValue >= 14) {
                score += 3;
            }

            // Neutrophils % scoring for AAS
            const aasNeutrophilsPercentage = (aasNeutrophilsCountValue / aasWccValue) * 100;
            if (aasNeutrophilsPercentage < 62) {
                // Score remains 0
            } else if (aasNeutrophilsPercentage >= 62 && aasNeutrophilsPercentage <= 75) {
                score += 2;
            } else if (aasNeutrophilsPercentage > 75 && aasNeutrophilsPercentage <= 83) {
                score += 3;
            } else if (aasNeutrophilsPercentage > 83) {
                score += 4;
            }

            score += getRadioValue('aas-crp');

            scoreValueSpan.textContent = score;
            let interpretation = '';
            // Updated interpretation based on user request
            if (score <= 8) {
                interpretation = `Low Risk of appendicitis (AAS Score: ${score}).`;
            } else if (score >= 9) {
                interpretation = `Medium to High Risk of appendicitis (AAS Score: ${score}). Consider further clinical evaluation.`;
            }
            scoreInterpretationParagraph.textContent = interpretation;
            resultsDisplay.classList.remove('hidden');
        }


        function calculateAIRSScore() {
            let score = 0;
            const age = parseInt(airsAgeSelect.value, 10);

            if (isNaN(age)) {
                scoreValueSpan.textContent = '';
                scoreInterpretationParagraph.textContent = 'Please select patient\'s age.';
                resultsDisplay.classList.remove('hidden');
                return;
            }

            // Get slider values - Use parseFloat
            const airsWccValue = parseFloat(airsWccSlider.value);
            const airsNeutrophilsCountValue = parseFloat(airsNeutrophilsCountSlider.value);

            // Validate slider values for calculation
            if (isNaN(airsWccValue) || isNaN(airsNeutrophilsCountValue)) {
                scoreValueSpan.textContent = '';
                scoreInterpretationParagraph.textContent = 'Please provide values for Total WCC and Neutrophils Count.';
                resultsDisplay.classList.remove('hidden');
                return;
            }
            if (airsWccValue === 0) { // Prevent division by zero
                scoreValueSpan.textContent = '';
                scoreInterpretationParagraph.textContent = 'Total WCC cannot be zero for neutrophil percentage calculation.';
                resultsDisplay.classList.remove('hidden');
                return;
            }

            // Check if all required radio questions are answered for AIRS
            const requiredAirsRadioQuestions = [
                'airs-vomiting',
                'airs-rif-pain',
                'airs-rebound-tenderness',
                'airs-temp',
                'airs-crp'
            ];
            let allAirsRadiosAnswered = true;
            for (const qName of requiredAirsRadioQuestions) {
                if (getRadioValue(qName) === null) {
                    allAirsRadiosAnswered = false;
                    break;
                }
            }

            if (!allAirsRadiosAnswered) {
                scoreValueSpan.textContent = '';
                scoreInterpretationParagraph.textContent = 'Please answer all questions to calculate the score.';
                resultsDisplay.classList.remove('hidden');
                return;
            }

            // AIRS Score calculation logic based on PDF
            score += getRadioValue('airs-vomiting');
            score += getRadioValue('airs-rif-pain');
            score += getRadioValue('airs-rebound-tenderness');
            score += getRadioValue('airs-temp');
            
            // WCC scoring
            if (airsWccValue >= 10 && airsWccValue <= 14.9) {
                score += 1;
            } else if (airsWccValue >= 15) {
                score += 2;
            }

            // Neutrophils % scoring
            const neutrophilsPercentage = (airsNeutrophilsCountValue / airsWccValue) * 100;
            if (neutrophilsPercentage >= 70 && neutrophilsPercentage <= 84) {
                score += 1;
            } else if (neutrophilsPercentage >= 85) {
                score += 2;
            }

            score += getRadioValue('airs-crp');

            scoreValueSpan.textContent = score;
            let interpretation = '';
            // Updated interpretation based on user request
            if (score <= 2) {
                interpretation = `Low Risk of appendicitis (AIRS Score: ${score}).`;
            } else if (score >= 3) {
                interpretation = `Medium to High Risk of appendicitis (AIRS Score: ${score}).`;
            } 
            scoreInterpretationParagraph.textContent = interpretation;
            resultsDisplay.classList.remove('hidden');
        }


        // --- Event Listeners ---

        // Listen for gender selection
        document.querySelectorAll('input[name="gender"]').forEach(radio => {
            radio.addEventListener('change', (event) => {
                const selectedGender = event.target.value;
                scoreValueSpan.textContent = ''; // Clear score when switching gender
                scoreInterpretationParagraph.textContent = ''; // Clear interpretation
                resultsDisplay.classList.add('hidden'); // Hide results until form is filled

                if (selectedGender === 'female') {
                    aasForm.classList.remove('hidden');
                    airsForm.classList.add('hidden');
                    resetForm('airs-form'); // Reset AIRS form if previously shown
                    calculateAASScore(); // Calculate initial score for AAS if gender is selected
                } else if (selectedGender === 'male') {
                    airsForm.classList.remove('hidden');
                    aasForm.classList.add('hidden');
                    resetForm('aas-form'); // Reset AAS form if previously shown
                    calculateAIRSScore(); // Calculate initial score for AIRS if gender is selected
                }
            });
        });

        // Add event listeners for AAS form inputs (radio buttons)
        aasForm.querySelectorAll('input[type="radio"]').forEach(radio => {
            radio.addEventListener('change', calculateAASScore);
        });

        // Add event listeners for AIRS form inputs (radio buttons)
        airsForm.querySelectorAll('input[type="radio"]').forEach(radio => {
            radio.addEventListener('change', calculateAIRSScore);
        });

        // Listen for AAS Symptom Duration change to show/hide CRP sections and recalculate
        document.querySelectorAll('input[name="aas-symptom-duration"]').forEach(radio => {
            radio.addEventListener('change', (event) => {
                const duration = event.target.value;
                if (duration === 'less-24') {
                    aasCrpLess24.style.display = 'block';
                    aasCrpGreater24.style.display = 'none';
                    document.querySelectorAll('#aas-crp-greater-24 input[name="aas-crp"]').forEach(radio => radio.checked = false);
                } else if (duration === 'greater-24') {
                    aasCrpLess24.style.display = 'none';
                    aasCrpGreater24.style.display = 'block';
                    document.querySelectorAll('#aas-crp-less-24 input[name="aas-crp"]').forEach(radio => radio.checked = false);
                }
                calculateAASScore(); // Recalculate after duration selection
            });
        });


        // Manual Calculate buttons (will now primarily serve as validation check)
        calculateAasBtn.addEventListener('click', calculateAASScore);
        calculateAirsBtn.addEventListener('click', calculateAIRSScore);


        // Reset AAS Form
        resetAasBtn.addEventListener('click', () => {
            resetForm('aas-form');
            document.querySelectorAll('input[name="gender"]').forEach(radio => radio.checked = false);
            genderSelection.classList.remove('hidden');
            aasForm.classList.add('hidden'); // Hide after reset
        });

        // Reset AIRS Form
        resetAirsBtn.addEventListener('click', () => {
            resetForm('airs-form');
            document.querySelectorAll('input[name="gender"]').forEach(radio => radio.checked = false);
            genderSelection.classList.remove('hidden');
            airsForm.classList.add('hidden'); // Hide after reset
        });

        // Reset All (from results screen)
        resetAllBtn.addEventListener('click', () => {
            resetForm('aas-form');
            resetForm('airs-form');
            resetChecklist();
            document.querySelectorAll('input[name="gender"]').forEach(radio => radio.checked = false); // Clear gender selection
            genderSelection.classList.remove('hidden');
            resultsDisplay.classList.add('hidden');
        });

        // Reset Checklist button
        document.getElementById('reset-checklist').addEventListener('click', resetChecklist);


        // --- Custom Message Box Implementation (replaces alert()) ---
        function displayMessage(message, type) {
            // Create modal elements
            const modalOverlay = document.createElement('div');
            modalOverlay.classList.add('fixed', 'inset-0', 'bg-gray-600', 'bg-opacity-50', 'flex', 'items-center', 'justify-center', 'z-50');

            const modalContent = document.createElement('div');
            modalContent.classList.add('bg-white', 'p-6', 'rounded-lg', 'shadow-xl', 'max-w-sm', 'mx-auto', 'text-center');

            const title = document.createElement('h3');
            title.classList.add('text-xl', 'font-bold', 'mb-3');
            title.textContent = type;
            if (type === "Error") {
                title.classList.add('text-red-600');
            } else {
                title.classList.add('text-blue-600');
            }

            const messagePara = document.createElement('p');
            messagePara.classList.add('text-gray-700', 'mb-4');
            messagePara.textContent = message;

            const closeButton = document.createElement('button');
            closeButton.classList.add('btn', 'btn-primary');
            closeButton.textContent = 'OK';
            closeButton.addEventListener('click', () => {
                document.body.removeChild(modalOverlay);
            });

            modalContent.appendChild(title);
            modalContent.appendChild(messagePara);
            modalOverlay.appendChild(modalContent);
            document.body.appendChild(modalOverlay);
        }

        // --- Copy Summary to Clipboard Function ---
        copyAnswersBtn.addEventListener('click', copySummaryToClipboard);

        function copySummaryToClipboard() {
            let summaryText = "--- Appendicitis Risk Stratification Summary ---\n\n";

            // 1. Patient Gender and Score
            const selectedGenderRadio = document.querySelector('input[name="gender"]:checked');
            if (selectedGenderRadio) {
                const gender = selectedGenderRadio.value.charAt(0).toUpperCase() + selectedGenderRadio.value.slice(1);
                summaryText += `Patient Gender: ${gender}\n`;
                summaryText += `Calculated Score: ${scoreValueSpan.textContent || 'N/A'}\n`;
                summaryText += `Risk Level: ${scoreInterpretationParagraph.textContent || 'N/A'}\n\n`;
            } else {
                summaryText += "Patient Gender: Not selected\n";
                summaryText += "Calculated Score: N/A\n";
                summaryText += "Risk Level: N/A\n\n";
            }

            // 2. Checklist Summary
            summaryText += "--- Clarity Checklist Summary ---\n";
            const checklistSteps = [
                { id: 'step1-completed', label: 'Step 1: Risk Stratification' },
                { id: 'step2-completed', label: 'Step 2: Care Pathway' },
                { id: 'step3-completed', label: 'Step 3: Selective Imaging' },
                { id: 'step4-completed', label: 'Step 4: Management' }
            ];

            checklistSteps.forEach(step => {
                const checkbox = document.getElementById(step.id);
                const status = checkbox && checkbox.checked ? 'Completed' : 'Not Completed';
                summaryText += `${step.label}: ${status}\n`;
            });

            // Copy to clipboard
            const textarea = document.createElement('textarea');
            textarea.value = summaryText;
            document.body.appendChild(textarea);
            textarea.select();
            try {
                document.execCommand('copy');
                displayMessage('Summary copied to clipboard!', 'Success');
            } catch (err) {
                displayMessage('Failed to copy summary. Please try manually.', 'Error');
            }
            document.body.removeChild(textarea);
        }

    </script>
</body>
</html>
