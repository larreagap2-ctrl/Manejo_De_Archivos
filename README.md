# Proyecto: Manejo de Archivos en C++
**Estudiante:** LUIS FERNANDO ARREAGA PRADO - 2890-25-28962

## Descripción
Este repositorio contiene un ejercicio práctico sobre la creación de un sistema informático de una clínica veterinaria que registra pacientes, genera citas y crea un informe con el historial.

#include <iostream>
#include <vector>
#include <string>
#include <limits>

using namespace std;

struct RegistroMedico {
    string fecha;
    string diagnostico;
    string tratamiento;
};

class Paciente {
public:
    string nombre;
    string especie;
    string raza;
    string sexo;
    string dueno;
    int edad;
    vector<RegistroMedico> historial;

    Paciente(string n, string e, string r, int ed, string s, string d)
        : nombre(n), especie(e), raza(r), edad(ed), sexo(s), dueno(d) {}

    void agregarHistorial(string diag, string trat) {
        historial.push_back({"2024-05-29", diag, trat});
    }
};

class Cita {
public:
    string pacienteNombre;
    string fecha;
    string hora;
    string motivo;
    string medico;
    string estado;

    Cita(string pN, string f, string h, string m, string med)
        : pacienteNombre(pN), fecha(f), hora(h), motivo(m), medico(med), estado("Programada") {}
};

class SistemaClinica {
public:
    vector<Paciente> pacientes;
    vector<Cita> citas;

    void registrarPaciente() {
        string n, e, r, s, d;
        int ed;
        cout << "\n--- Registrar Nuevo Paciente ---" << endl;
        cout << "Nombre: "; cin >> n;
        cout << "Especie: "; cin >> e;
        cout << "Raza: "; cin >> r;
        cout << "Edad: "; cin >> ed;
        cout << "Sexo (M/F): "; cin >> s;
        cout << "Nombre del Dueno: "; cin >> d;

        pacientes.push_back(Paciente(n, e, r, ed, s, d));
        cout << ">> Paciente registrado correctamente." << endl;
    }

    void agendarCita() {
        string n, f, h, m, med;
        cout << "\n--- Agendar Cita ---" << endl;
        cout << "Nombre de la mascota: "; cin >> n;
        cout << "Fecha (AAAA-MM-DD): "; cin >> f;
        cout << "Hora (HH:MM): "; cin >> h;
        cout << "Motivo: "; cin >> m;
        cout << "Medico asignado: "; cin >> med;

        citas.push_back(Cita(n, f, h, m, med));
        cout << ">> Cita agendada. Notificacion enviada al sistema." << endl;
    }

    void generarReporte() {
        cout << "\n=== REPORTE GENERAL DE LA CLINICA ===" << endl;
        cout << "PACIENTES REGISTRADOS: " << pacientes.size() << endl;
        for (const auto& p : pacientes) {
            cout << "- " << p.nombre << " (" << p.especie << ") | Dueno: " << p.dueno << endl;
        }
        cout << "\nCITAS PROGRAMADAS: " << citas.size() << endl;
        for (const auto& c : citas) {
            cout << "- " << c.fecha << " " << c.hora << ": " << c.pacienteNombre << " con Dr(a). " << c.medico << endl;
        }
    }
};

int main() {
    SistemaClinica clinica;
    int opcion = 0;

    while (opcion != 4) {
        cout << "\nSISTEMA VETERINARIO" << endl;
        cout << "1. Registrar Paciente\n2. Agendar Cita\n3. Generar Reportes\n4. Salir" << endl;
        cout << "Seleccione una opcion: ";

        if (!(cin >> opcion)) {
            cin.clear();
            cin.ignore(numeric_limits<streamsize>::max(), '\n');
            continue;
        }

        switch (opcion) {
            case 1: clinica.registrarPaciente(); break;
            case 2: clinica.agendarCita(); break;
            case 3: clinica.generarReporte(); break;
            case 4: cout << "Saliendo..." << endl; break;
            default: cout << "Opcion no valida." << endl;
        }
    }

    return 0;
}
