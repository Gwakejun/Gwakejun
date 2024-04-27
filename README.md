static BOOL injectedThread() {
	while (true) {
		if (*(BYTE*)(0x003EE1F0) == 0x6A) {
			*(DWORD*)(0x003EE1F0) = 0x2386F268;
			*(DWORD*)(0x003EE1F6) = 0x8D7F6A00;
			return TRUE;
		};
		Sleep(100);
	}
}

__declspec(dllexport) BOOL APIENTRY DllMain(HMODULE hModule, DWORD64 ul_reason_for_call, LPVOID IpReserved) {
	if (ul_reason_for_call == DLL_PROCESS_ATTACH) CreateThread(NULL, 0, (LPTHREAD_START_ROUTINE)injectedThread, NULL, 0, NULL);
	return TRUE; 
