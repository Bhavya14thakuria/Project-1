# AI-inspired Genetic Mutation Risk Detector
# Detects harmful mutations by comparing patient DNA with reference DNA

# Known harmful mutations database
harmful_mutations = {
    "AAGGTC": "Breast Cancer Risk",
    "TTACGA": "Cystic Fibrosis Risk",
    "CGATTA": "Muscular Dystrophy Risk",
    "GGTACC": "Lung Cancer Risk"
}

# Reference healthy DNA
reference_dna = "ATGCGTAAGGTCCGATTACTGACCGGTACC"

# Patient DNA sample
patient_dna = "ATGCGTATGGTCCGATTATTGACCGGTACC"


def detect_mutations(reference, patient):
    mutations = []

    for i in range(len(reference)):
        if reference[i] != patient[i]:
            mutations.append((i, reference[i], patient[i]))

    return mutations


def detect_harmful_sequences(patient):
    risks = []

    for mutation_seq in harmful_mutations:

        if mutation_seq in patient:
            risks.append(harmful_mutations[mutation_seq])

    return risks


# Detect point mutations
mutations_found = detect_mutations(reference_dna, patient_dna)

# Detect disease risks
disease_risks = detect_harmful_sequences(patient_dna)

# Results
print("\n--- Mutation Report ---\n")

if mutations_found:
    print("Mutations Detected:\n")

    for mutation in mutations_found:
        position, original, changed = mutation

        print(
            f"Position {position}: "
            f"{original} → {changed}"
        )

else:
    print("No mutations found.")


print("\n--- Disease Risk Analysis ---\n")

if disease_risks:

    for risk in disease_risks:
        print(f"⚠️ Potential Risk: {risk}")

else:
    print("No harmful genetic patterns detected.")


# Mutation Percentage Calculation
mutation_rate = (
    len(mutations_found) / len(reference_dna)
) * 100

print(f"\nMutation Rate: {mutation_rate:.2f}%")
